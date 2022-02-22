---
layout: post
title: DCGAN 연습
date: 2022-02-22 00:00:00 +0900
category: dl_project
---

# DCGAN

아래 깃 허브의 코드를 참고하여 구현 연습을 하였다. <br>
https://github.com/Natsu6767/DCGAN-PyTorch

gan이 나온 후 

---
## DCGAN 구조

### 전체 구조

```bash
├── checkpoint
├── history
├── result
├── config.py 
├── data.py
├── generate.py
├── main.py
├── model.py
└── train.py
``` 

> - checkpoint : autosaved된 모델<br>
> - history : train의 error 기록<br>
> - result : latent vector를 연산하여 합성한 이미지 <br>
> - config.py : 여러 파라미터 모음<br>
> - data.py : celeba 데이터셋 불러오기<br>
> - generate.py : 이미지 합성 관련<br>
> - main.py<br>
> - model.py : Generator, Discriminator 정의<br>
> - train.py : train 함수<br>

하다 보니 구조가 위와 같이 되었다.

train을 따로 빼놓은 것은 train시 generator와 discriminator를 둘 다 학습해야 하기 때문이다. generate는 굳이 따로 빼지 않고, Generator 객체의 멤버함수로 가지고 있어도 될 것 같다.

몇가지 모델을 구현하다보니 대부분의 모델은 data, model, main로 나눠졌다. 이때 main에서 data와 model을 불러와서 하면 된다. 나중에 모든 코드를 이 3가지로 나눠서 정리하고 싶다.


### Main

> - model을 선언
> - optimizer를 선언 (model의 parameter를 등록해야 돼서 model 선언 후에 해야함)
> - history 선언
> - data 불러옴
> - train 하고 모든 epoch의 모델 저장
> - 학습한 generator로 이미지 합성

```python
# main.py

from model import *
from train import train
from generate import *
from config import *
from utils.history_manage import *

def main():
    '''
    마지막으로 autosaved된 model 불러온다. Generator랑 Discriminator를 불러온다.
    gan은 최적의 모델을 정할 수 있는 기준이 없다. 
    그래서 일단은 마지막으로 autosaved된 모델을 불러왔다.
    '''
    loaded_model, last_epoch = get_last_model()

    netG = Generator(params).to(device)

    if loaded_model == None:
        netG.apply(weights_init)
    else:
        netG.load_state_dict(loaded_model['generator'])

    netD = Discriminator(params).to(device)

    if loaded_model == None:
        netD.apply(weights_init)
    else:
        netD.load_state_dict(loaded_model['discriminator'])

    # optimizer 선언
    optimizerD = optim_D(netD.parameters(), lr=params['lr'], betas=(params['beta1'], params['beta2']))
    optimizerG = optim_G(netG.parameters(), lr=params['lr'], betas=(params['beta1'], params['beta2']))

    # history는 train 할 때 계산되는 error를 csv파일로 저장하기 위해 만들었다.
    history = ValueHistory()

    # celebA 데이터셋을 불러온다.
    dataloader = get_celeba(params)
    for epoch in range(params['nepochs']):
        train(netD, netG, optimizerD, optimizerG, dataloader, history, epoch, last_epoch + 1)
        # 가장 최적의 모델을 알 수 없으니 일단 모든 epoch의 모델을 저장했다.
        history.save_csv_all_history(f"train_err_{epoch + last_epoch + 1}", "../history")

    # 학습한 generator로 1개의 random으로 생성된 latent vector로 1개의 이미지를 합성
    generate(1, netG)
    # 학습한 generator로 10개의 random으로 생성된 latent vector에 interpolation을 추가한 후 이미지를 합성
    generate_gradation_with_interpolation(10, netG)
    # 학습한 generator로 30개의 random으로 생성된 latent vector를 더하고 빼서 새로운 letent vector를 만든 다음 10개 이미지를 합성
    generate_with_calculated_context_vector(10, netG)

if __name__ == '__main__':
    main()

```

### Model

model에는 generator와 discriminator를 정의한다.

```python
class Generator(nn.Module):
    def __init__(self, params):
        super().__init__()

        self.tconv1 = nn.ConvTranspose2d(params['nz'], params['ngf']*8,
            kernel_size=4, stride=1, padding=0, bias=False)
        self.bn1 = nn.BatchNorm2d(params['ngf']*8)

        self.tconv2 = nn.ConvTranspose2d(params['ngf']*8, params['ngf']*4,
            4, 2, 1, bias=False)
        self.bn2 = nn.BatchNorm2d(params['ngf']*4)

        self.tconv3 = nn.ConvTranspose2d(params['ngf']*4, params['ngf']*2,
            4, 2, 1, bias=False)
        self.bn3 = nn.BatchNorm2d(params['ngf']*2)

        self.tconv4 = nn.ConvTranspose2d(params['ngf']*2, params['ngf'],
            4, 2, 1, bias=False)
        self.bn4 = nn.BatchNorm2d(params['ngf'])

        self.tconv5 = nn.ConvTranspose2d(params['ngf'], params['nc'],
            4, 2, 1, bias=False)

    def forward(self, x):
        x = F.relu(self.bn1(self.tconv1(x)))
        x = F.relu(self.bn2(self.tconv2(x)))
        x = F.relu(self.bn3(self.tconv3(x)))
        x = F.relu(self.bn4(self.tconv4(x)))

        x = F.tanh(self.tconv5(x))

        return x
```


```python
class Discriminator(nn.Module):
    def __init__(self, params):
        super().__init__()

        self.conv1 = nn.Conv2d(params['nc'], params['ndf'],
            4, 2, 1, bias=False)

        self.conv2 = nn.Conv2d(params['ndf'], params['ndf']*2,
            4, 2, 1, bias=False)
        self.bn2 = nn.BatchNorm2d(params['ndf']*2)

        self.conv3 = nn.Conv2d(params['ndf']*2, params['ndf']*4,
            4, 2, 1, bias=False)
        self.bn3 = nn.BatchNorm2d(params['ndf']*4)

        self.conv4 = nn.Conv2d(params['ndf']*4, params['ndf']*8,
            4, 2, 1, bias=False)
        self.bn4 = nn.BatchNorm2d(params['ndf']*8)

        self.conv5 = nn.Conv2d(params['ndf']*8, 1, 4, 1, 0, bias=False)

    def forward(self, x):
        x = F.leaky_relu(self.conv1(x), 0.2, True)
        x = F.leaky_relu(self.bn2(self.conv2(x)), 0.2, True)
        x = F.leaky_relu(self.bn3(self.conv3(x)), 0.2, True)
        x = F.leaky_relu(self.bn4(self.conv4(x)), 0.2, True)

        x = F.sigmoid(self.conv5(x))

        return x
```

---
## 결과
