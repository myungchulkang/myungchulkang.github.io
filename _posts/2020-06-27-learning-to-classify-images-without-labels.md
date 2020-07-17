---
title: "📄Learning to Classify Images Without Labels 논문 리뷰"
date: 2020-06-27
tags:
---

# 들어가기에 앞서

- 논문: Learning to Classify Images Without Labels

- URL: [https://arxiv.org/abs/2005.12320](https://arxiv.org/abs/2005.12320)

저번에 74페이지인가 하는 GPT-3논문을 처음부터 한 섹션씩 정리하려니까 2장까지 하는 데에도 너무 많은 시간이 걸렸다. 이제부터는 논문의 핵심 아이디어만 빠르게 skim하면서 블로그에 정리하고, 좋은 논문임이 판단되면 자세하게 살펴보려고 한다. 물론 이제까지 그래왔지만 이렇게 블로그에 정리를 하면서 논문을 읽으니 더 오래 걸린다 ㅋㅋ

이번에는 해당 유튜브 채널에서 먼저 짚어주는 포인트들을 살펴보고, 그 다음에 나의 관점에서 논문을 보려고 한다.

- Yannic Kilcher: [Learning To Classify Images Without Labels (Paper Explained)](https://www.youtube.com/watch?v=hQEnzdLkPj4&t=123s)

# 0.Abstract

과연 annotation 없이(레이블 없이) 이미지를 분류하는 것이 가능할까? 해당 논문에서는 다음의 핵심 아이디어를 통해 가능하다고 한다.

1. self-supervised learning
2. clustering
3. self-labeling

어떠한 NN을 통해서이든 잘 표현된 임베딩을 구한다.


여러 변형을 주고 같은 모델에 입력하였을 때 가장 마지막에 나오는 임베딩 값으로 K개의 주변 임베딩을 살펴보니 이미 그 이미지가 비슷했다.

그러나 이걸로는 부족하고 self-labeling을 통해 다시 학습한다. 내가 나의 데이터에 레이블링하는 것이 어떤 의미가 있을까? 그러나 정교하게 하는 것은 의미가 있다.

질문) 그런데 무슨 task를 통해서 마지막 값을 찾을거지?

그런데 결국 성능 측정은 ground-truth에 대해 하는 것인데 의미가 있나..? 노노 그래도 레이블 없이 사용하는 것이 높은 정확도를 보이니 앞으로는 없이 그냥 그 임베딩 값을 사용해도 된다.

그러나 많은 hyperparameter 가 많이 있다.. pretext model, threshold, .. 문제는 이러한 파라미터들이 결국은 레이블을 알고 있어야 어느 정도 정할 수 있다는 딜레마에 빠지게 된다.
