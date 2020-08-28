---
title: "anaconda 재설치 및 python과 anaconda 차이"
date: 2020-08-28
tags: python anaconda
---

## 문제점
댓글 데이터 전처리 과정 중에 pykospacing가 import가 안되는 문제가 생기고, 맞춤법 검사기 또한 json 파일 관련 문제가 발생했다..
또한 커널이 지속적으로 멈춘다...

[여기](https://github.com/jupyter/notebook/issues/1892)에서 알려주는 방법들을 모두 시도해보았으나 해결되지 않았다. 그래서 아예 anaconda를 지우고 새로 설치하려고 한다. anaconda를 지우는 방법은 [공식 사이트](https://docs.anaconda.com/anaconda/install/uninstall/)에 잘 나와있다.

우선 `anaconda-clean` 패키지를 설치하고 실행하여 모든 관련 파일들(패키지, 커널, ...)을 하나의 백업 파일로 만들어 준 후 한 번에 삭제하면 된다. 그 후 또 다시 공식 홈페이지에서 알려주는대로 설치를 진행하면 된다. -끝-

진행하던 중 anaconda를 설치하면 python을 설치하지 않아도 되나? 하는 궁금증이 생겨 또 다시 검색해보았다.(모든 답은 구글형이 알고 있다.)

[여기서](https://snowdeer.github.io/python/2017/11/07/python-vs-anaconda/) 찾을 수 있었는데, 요약하자면: 환경 변수 충돌 등의 문제가 있을 수 있기 때문에 python과 anaconda 중 하나만 설치하는 것이 바람직하다고 한다.

하지만, pandas와 numpy 등 데이터분석에 반드시 활용되는 패키지들을 가지고 있는 anaconda를 설치하는 것을 권장한다.

![python-and-anaconda](/assets/python-and-anaconda_5ccy9hdx7.PNG)

그 이후 패키지 설치하는데에는 다음과 같은 방법이 있다. [여기](https://dailyheumsi.tistory.com/33)와 [여기](http://hleecaster.com/installing-python-anaconda/).

요약하자면: 가상환경을 만들고 거기에 설치할 때는 `pip install` 든 `conda install`이든 무관하다. `pip3 install`을 하면 전역(base)에 설치되니 `pip install`로 하자.

## 출처
- https://snowdeer.github.io/python/2017/11/07/python-vs-anaconda/
- https://dailyheumsi.tistory.com/33
- http://hleecaster.com/installing-python-anaconda/
- https://docs.anaconda.com/anaconda/install/uninstall/
