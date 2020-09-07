---
title: "[코딩정복🎮] 에러 노트"
date: 2020-09-07
tags: code
---

## 들어가기에 앞서
코딩 입문자인 나는 매일 같이 수도 없이 많은 에러를 마주친다. 물론 새로운 작업을 할 때는 새로운 에러를 만나는 편이지만 과거에 보았던 같은 에러를 또 다시 만는 경우도 있다. 이럴 때 같은 실수를 반복하지 않고 빠르게 해결할 수 있도록 미래의 나를 위해 만났던 에러들을 여기에 기록해 두려고 한다.

해당 에러의 제목은 목차로 정리됨으로 번호를 붙이지 않고, 현상/해결 과정/결론(+출처)에만 번호를 사용하여 지속적으로 정리할 계획이다. 일정 수준 이상의 에러를 기록하면 증상 별로 다시 정리할 것이다. ~~물론 그 만큼 쌓일 정도로 성실하게 포스팅할 수 있을 지는 미지수~~

## 코랩에서 한글 깨짐 에러
### 1. 현상
프로젝트 진행 중 다음과 같이 코랩에서 한글로 작성된 txt 파일을 불러왔는데 몽땅 깨져있었다 ㅠㅠ

![코랩 한글 깨짐 현상](/assets/코랩%20한글%20깨짐%20현상.PNG)

### 2. 해결 과정

[여기](https://teddylee777.github.io/pandas/%EA%B3%B5%EA%B3%B5%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%95%9C%EA%B8%80%EA%B9%A8%EC%A7%90%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)를 우선 참고 하였다.

엑셀 파일에서 열심히 인코딩을 변경해보았으나 해결되지 않았다. 여러 방법으로 해보던 도중 해결 방법은 생각보다 단순했다. txt 파일의 인코딩을 바꿔주고!! 코랩에 업로드하면 됐던 것이다!

![텍스트-파일-인코딩-변경](/assets/텍스트-파일-인코딩-변경.PNG)

### 3. 결론과 출처

- 인코딩을 변경하는 방법은 다양하다: 엑셀에서 "데이터 불러오기"에서 변경 / 엑셀에서 "다른 이름으로 저장" / 텍스트 파일에서 직접 인코딩 변경
- https://teddylee777.github.io/pandas/%EA%B3%B5%EA%B3%B5%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%95%9C%EA%B8%80%EA%B9%A8%EC%A7%90%ED%98%84%EC%83%81-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95