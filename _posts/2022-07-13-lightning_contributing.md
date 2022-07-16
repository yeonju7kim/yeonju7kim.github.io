---
layout: post
title: Lightning contribution
date: 2022-07-13 00:00:00 +0900
category: lightning_ai
use_math: true
comments: true
---

# Lightning contribution

예전부터 open source contribution을 해보고 싶은 생각이 있었는데, 오픈소스 컨트리뷰션 아카데미라는 프로그램을 알게 돼서 멘토의 도움을 받아서 open source에 기여하는 경험을 할 수 있는 기회가 생겼다. 여러가지 프로젝트 중에 하나를 선택해야했는데, 나는 lightning ai라는 pytorch를 추상화하는 python package를 수정하는 프로젝트를 하게 되었다.

[lightning ai](https://github.com/Lightning-AI/lightning) 깃에 들어가보면 프로젝트가 잘 관리되고 있는 것을 볼 수 있다. 지금까지 개발 문화 경험을 많이 못해봤는데, 이 프로젝트를 보니 contributing 할 때 유의사항이라든지, doc이나 code style에 대한 convention에 대해서도 적어놓은 것을 보고 신기했다.

아래는 contributing 할 때의 유의사항을 읽고 요약한 것이다. 내가 읽으려고 요약해놓은 것이기 때문에 다른 사람들이 보기에 어려울 수도 있다.

---

## About the project

- Main Core Value : One less thing to remember
- Lightning Design principle
  - No PyTorch Interference
  - Simple Internal Code
  - Force User Decisions To Best Practices
  - Simple External API
  - Backward-compatible API
    - good deprecation warnings.
  - Gain User Trust
  - Interoperability

## Contribution

- Contribution types
  1. bug fixes
>
> - bug issue
>   - title
>   - setup(config, code sample)
>   - how to reproduce the issue
> - fix or recommend w/ test-driven approach
>   - minimal code convert w/ unit/integration test
>   - test your test case on master branch and fixed code
> - PR


  2. new features
>
>- issue
> - motivation
> - discuss about the scope
> - PR
>   - testcode + functional code

- Guideline
  - Developments scripts(UNIX)
  - Original code
    - refer the 3rd party implementation
  - coding style
    - Use f-strings for output formation
    - Use pre-commit
  - Docs
    - https://github.com/Lightning-AI/lightning/blob/master/docs/README.md
  - test
    - https://github.com/Lightning-AI/lightning/blob/master/tests/README.md
  - Pull Request
    - If your PR is not ready for reviews, but you want to run it on our CI, open a "Draft PR" to let us know you don't need feedback yet.
  - branch name
    - type/issue-id_short-name (types : bugfix, feature, docs, or tests)
    - 
## Reference

<https://github.com/Lightning-AI/lightning/blob/562467402d0e58ff8661b9260ed0fb21f935eb93/.github/CONTRIBUTING.md>
