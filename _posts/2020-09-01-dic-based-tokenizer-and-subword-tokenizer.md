---
title: "사전 기반 tokenizer Vs. Subword tokenizer"
date: 2020-09-01
tags: tokenizer 개념정리
---
## 들어가기에 앞서

이번 포스트에서는 토큰나이져에 대해 알아보자.

세미나 자료 확인 [LangCon2020](https://songys.github.io/2020LangCon/about/)과 [허훈 님의 블로그](https://huffon.github.io/2020/07/05/tokenizers/)를 그대로 가져와 정리하는 식으로 작성하였다.


## 토크나이저(tokenizer)란?

문장을 작은 단위로 쪼개는 것을 토큰화 한다고 하며 이를 수행할때 사용하는 것을 토크나이저라고 한다.

![토크나이저비교](/assets/images/토크나이저비교.PNG)

기본적으로 '시전 기반'과 'Subword 기반' 토크나이저가 있고 차이점은 다음과 같다. 두 종류의 토크나이저는 각자의 장단점도. 사용 목적도 서로 다르다.

- Subword 토크나이저는 자주 등장하는 단어를 제대로 인식할 가능성이 높지만,
- 빈번하지 않는 단어는 사전 기반 토크나이저가 잘 인식한다.
- 전체 단어의 개수가 제한된 상황에서는 사전 기반 방식으로 인식된 다수의 단어를 `<unk>`로 처리해야 하지만, Subword 토크나이저는 알려진 글자로 분해하여 `<unk>`의 개수를 줄인다.

Subword 토크나이저는 [huggingface](https://huggingface.co/transformers/master/tokenizer_summary.html#)에서 제공하는 네 가지의 종류가 있다.

![huggingface에서 제공해주는 토크나이저](/assets/images/huggingface에서%20제공해주는%20토크나이저.PNG)

## 출처

- https://songys.github.io/2020LangCon/about/
- https://huffon.github.io/2020/07/05/tokenizers/
- https://huggingface.co/transformers/master/tokenizer_summary.html#
