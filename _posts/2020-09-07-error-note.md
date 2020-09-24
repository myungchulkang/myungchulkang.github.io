---
title: "에러 노트 (항상 업데이트중)"
date: 2020-09-07
tags: code
---

## 들어가기에 앞서
코딩 입문자인 나는 매일 같이 수도 없이 많은 에러를 마주친다. 물론 새로운 작업을 할 때는 새로운 에러를 만나는 편이지만 과거에 보았던 같은 에러를 또 다시 만는 경우도 있다. 이럴 때 같은 실수를 반복하지 않고 빠르게 해결할 수 있도록 미래의 나를 위해 만났던 에러들을 여기에 기록해 두려고 한다.

해당 에러의 제목은 목차로 정리됨으로 번호를 붙이지 않고, 현상/해결 과정/결론(+출처)에만 번호를 사용하여 지속적으로 정리할 계획이다. 일정 수준 이상의 에러를 기록하면 증상 별로 다시 정리할 것이다. ~~물론 그 만큼 쌓일 정도로 성실하게 포스팅할 수 있을 지는 미지수~~

## 코랩에서 한글 깨짐 에러
### 1. 현상
프로젝트 진행 중 다음과 같이 코랩에서 한글로 작성된 txt 파일을 불러왔는데 몽땅 깨져있었다 ㅠㅠ

![코랩 한글 깨짐 현상](/assets/images/코랩%20한글%20깨짐%20현상.PNG)

### 2. 해결 과정

[여기](https://teddylee777.github.io/pandas/%EA%B3%B5%EA%B3%B5%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%95%9C%EA%B8%80%EA%B9%A8%EC%A7%90%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)를 우선 참고 하였다.

엑셀 파일에서 열심히 인코딩을 변경해보았으나 해결되지 않았다. 여러 방법으로 해보던 도중 해결 방법은 생각보다 단순했다. txt 파일의 인코딩을 바꿔주고!! 코랩에 업로드하면 됐던 것이다!

![텍스트-파일-인코딩-변경](/assets/images/텍스트-파일-인코딩-변경.PNG)

### 3. 결론과 출처

- 인코딩을 변경하는 방법은 다양하다: 엑셀에서 "데이터 불러오기"에서 변경 / 엑셀에서 "다른 이름으로 저장" / 텍스트 파일에서 직접 인코딩 변경
- https://teddylee777.github.io/pandas/%EA%B3%B5%EA%B3%B5%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%95%9C%EA%B8%80%EA%B9%A8%EC%A7%90%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95


## 코랩에서 RuntimeError: CUDA error: device-side assert triggered

### 1. 현상

KcBERT를 fine-tuning 하는 중 예제 코랩 파일에서 데이터셋만 바꿨을 뿐인데 위와 같은 오류가 발생했다.

### 2. 해결 과정

[한글 블로그](https://brstar96.github.io/shoveling/device_error_summary/)를 찾을 수 있었는데, 레이블 시작을 0으로 하는 등 여러가지를 시도했으나 해결하지 못했다.

[여기](https://stackoverflow.com/questions/53268442/pytorch-runtimeerror-cuda-error-device-side-assert-triggered)에서 코랩의 runtime type을 None으로 하면 실제 어떤 것이 문제가 되는지 알 수 있다고 한다.

> Switch Hardware Accelerator Type to `None` under `Runtime`->`Change Runtime Type`. This should give you a more meaningful error message.

`None`으로 변경하고 다시 돌려보니 에러가 달라져 있었다.

`IndexError: Target 2 is out of bounds.`

그래서 곧바로 해당 에러의 원인을 찾아보았다.

[여기](https://discuss.pytorch.org/t/indexerror-target-2-is-out-of-bounds/69614)를 살펴보니 target 크기의 문제인 것 같다.

[KcBERT 깃허브](https://github.com/Beomi/KcBERT/issues/3)에 이슈로 여쭤보니 `BertForSequenceClassification`은 기본적으로 `num_label=2` 라는 옵션을 가지고 있기 때문에, `num_label=5`로 지정해줘야한다고 한다.

해당 옵션을 적절히 추가한 후 만난 에러는 다음과 같다.

`RuntimeError: Error(s) in loading state_dict for BertForSequenceClassification`

이번에도 검색해보자. 사실 이건 다른 일과 동시에 하다보니 어떻게 해결했는지 까먹었다. ~~미래의 나, 미안~~ 아마도 metric가 default 값인 binary로 설정되어 있어서, 적절하게 바꿔주니 적어도 위의 에러는 사라졌던 것 같다 ㅎㅎ

그러자 또 다른 에러가 찾아옴..

`RuntimeError: DataLoader worker (pid 1619) is killed by signal: Killed.`

[여기](https://github.com/pytorch/pytorch/issues/8976)에서 해답을 찾을 수 있었다.

> You can try running with num_workers=0 and see if it gives you a better error (as it doesn't use subprocesses).

이렇게 `num_workers=0`으로 세팅하니 드디어 학습이 시작되었다!! 하지만 이게 과연 multi processing 입장에서 좋은 방법인지는 모르겠다. 우선 제한된 시간이기 때문에 빠르게 넘어가자!

### 3. 결론과 출처

- https://stackoverflow.com/questions/53268442/pytorch-runtimeerror-cuda-error-device-side-assert-triggere
- https://discuss.pytorch.org/t/indexerror-target-2-is-out-of-bounds/69614
- https://github.com/Beomi/KcBERT/issues/3
- https://github.com/pytorch/pytorch/issues/8976
