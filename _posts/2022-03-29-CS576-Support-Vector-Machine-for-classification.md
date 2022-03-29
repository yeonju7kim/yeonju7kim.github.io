---
layout: post
title: (CS576) Support Vector Machine for classification
date: 2022-03-29 00:10:00 +0900
category: class-summary
use_math: true
comments: true
---

본 포스팅은 CS576 수업에서 제가 새로 배운 부분만 정리한 것입니다.

---

## Support Vector Machine(SVM)

- Max-margin classifier
- ![alt image](/public/img/20220329/svm.png)
- ![alt image](/public/img/20220329/svm_margin.png)
- margin을 maximize해서 학습한다.
  - ![alt image](/public/img/20220329/svm_function.png)
  - ![alt image](/public/img/20220329/lagrangian.png)
    - convex optimizer의 regulation
    - 위 식으로 $\frac{\delta L_p}{\delta w} = 0$, $\frac{\delta L_p}{\delta b} = 0$를 만족하는 w와 b를 찾는다.
    - ![alt image](/public/img/20220329/svm_optimized.png)
    - ![alt image](/public/img/20220329/svm_objective.png)
    - 