---
title: "[코딩정복🎮] anaconda🐍 재설치 및 jupyter notebook 시작 경로 변경"
date: 2020-08-28
tags: python anaconda
---

## 커널 멈춤 문제
댓글 데이터 전처리 과정 중에 pykospacing가 import가 안되는 문제가 생기고, 맞춤법 검사기 또한 json 파일 관련 문제가 발생했다..
또한 커널이 지속적으로 멈춘다...

[여기](https://github.com/jupyter/notebook/issues/1892)에서 알려주는 방법들을 모두 시도해보았으나 해결되지 않았다. 그래서 아예 anaconda를 지우고 새로 설치하려고 한다. anaconda를 지우는 방법은 [공식 사이트](https://docs.anaconda.com/anaconda/install/uninstall/)에 잘 나와있다.

우선 `anaconda-clean` 패키지를 설치하고 실행하여 모든 관련 파일들(패키지, 커널, ...)을 하나의 백업 파일로 만들어 준 후 한 번에 삭제하면 된다. 그 후 또 다시 공식 홈페이지에서 알려주는대로 설치를 진행하면 된다. -끝-

진행하던 중 anaconda를 설치하면 python을 설치하지 않아도 되나? 하는 궁금증이 생겨 또 다시 검색해보았다.(모든 답은 구글형이 알고 있다.)

그 답은 [여기서](https://snowdeer.github.io/python/2017/11/07/python-vs-anaconda/) 찾을 수 있었다.

- 요약: 환경 변수 충돌 등의 문제가 있을 수 있기 때문에 python과 anaconda 중 하나만 설치하는 것이 바람직하다.

하지만, pandas와 numpy 등 데이터분석에 반드시 활용되는 패키지들을 가지고 있는 anaconda를 설치하는 것을 권장한다.

![python-and-anaconda](/assets/python-and-anaconda.PNG)

## 패키지 관리

그 이후 패키지 설치하는데에는 다음과 같은 방법이 있다. [여기](https://dailyheumsi.tistory.com/33)와 [여기](http://hleecaster.com/installing-python-anaconda/).

- 요약: 가상환경을 만들고 거기에 설치할 때는 `pip install` 든 `conda install`이든 무관하다. `pip3 install`을 하면 전역(base)에 설치되니 `pip install`로 하자.

## 쥬피터 노트북 시작 경로 변경

`jupyter notebook --generate-config`을 하고 생성된 파일 안에서 notebook_dir를 변경하는 등 여러 방법들을 찾아봤지만 다른 문제만 연속적으로 발생할 뿐이였다.

나는 개인적으로 jupyter notebook 파일의 [속성]에 들어가서 [대상(T)]에서 직접 경로를 추가하는 것이 하는 것이 가장 빠르고 쉬었다.

![jupyter_notebook_path](/assets/jupyter_notebook_path.PNG)


- 요약: 위의 그림처럼 그냥 [대상(T)]에 `%USERPROFILE%`를 지우고 해당 경로를 넣으면 된다. 그 이후 쥬피터 노트북을 다시 실행하면 지정해준 경로에서 시작된다! 다만 쥬피터 노트북이 아예 켜지질 않는다면 경로의 백슬래쉬(\\)를 보통 슬래쉬(/)로 바꾸고 시도해보자.



## 가상 환경 생성
작업을 하다보면 여러 패키지들이 충돌나는 경우가 많다. 그러므로 해당 프로젝트를 진행할 때마다 다른 가상 환경을 만들어 주어 관리하는 것이 바람직하다.

cmd 창에서 다음과 같은 순서로 생성한다.

- `conda create --name 프로젝트이름 python=3.7` 파이썬 버전을 경우에 맞게 지정해줘야한다.
- `conda activate 프로젝트이름`: 만든 가상 환경을 실행한다. 여기까지가 가상환경을 만들어주는 것이고, 쥬피터 노트북에서 활용하기 직접 설정을 바꾸기 위해서는 다음의 과정이 추가적으로 필요하다.
- `conda install ipkernel`
- `conda install nb_conda_kernels`

쥬피터 노트북을 다시 확인해보면 `프로젝트이름`으로 새로운 커널(가상 환경)이 추가 되어 있는 것을 볼 수 있다.


## 출처
- https://snowdeer.github.io/python/2017/11/07/python-vs-anaconda/
- https://dailyheumsi.tistory.com/33
- http://hleecaster.com/installing-python-anaconda/
- https://docs.anaconda.com/anaconda/install/uninstall/
