---
layout: post
title: "ML_note #3 Learning Technic"
date: 2017-12-23
excerpt: "Machine Learning"
tags:
- Deep Learning
ref:
- 밑바닥부터 시작하는 딥러닝
- https://github.com/WegraLee/deep-learning-from-scratch
comments: true
---
## 매개변수 갱신
#### SGD(확률적 경사 하강법)
- 기본 매개변수 갱신 모델
- 모든 데이터가 아닌 mini_batch사이즈로 학습(Stocastic)
- 오류함수에 대한 각각의 편미분한 값으로 경사 하강(Gradient Descent)

#### Momentum
- 관성에 따라 이동하던 방향의 성질이 다음 갱신에 영향을 줌
- SGD에 비하여 지그재그 정도가 덜함

#### AdaGrad
- 학습률 감소모델
- 학습률 조정변수 : h
- 과거 기울기 : $\frac{dL}{dW}$
- $h = h + (\frac{dL}{dW})^2$
- $W = W + \eta \frac{1}{\sqrt{h}}$

**RMSProp**<br>
AdaGrad는 과거의 기울기를 제곱하여 계속 더해가서 마지막에는 0이 됩니다. 하지만 RMSProp라는 방법은 먼 과거의 기울기는 서서히 잊고 새로운 기울기 정보를 크게 반영하여 그 문제를 해결합니다. 이를 지수이동평균(Exponential Moving Average)이라고 합니다.
{: .notice}

#### Adam
- AdaGrad + Momentum
- 학습률 감소 + 관성

---

## 가중치의 초깃값
#### 0 초깃값 (활성화함수 : sigmoid)
- 모든 가중치가 0으로 시작될 경우 역전파가 아예 이루어지지 않음

#### 정규분포 초깃값 (활성화함수 : sigmoid)
- 표준편차 1일 때 0과 1로 치우침
- 표준편차 0.1일 때 가운데로 치우침
- sigmoid함수의 미분값이 한 방향으로 몰아감 => 표현력의 제한

#### Xavier 초깃값 (활성화함수 : sigmoid)
- 표준편차가 $\frac{1}{\sqrt{n}}$ 인 초기값 (n = 앞 계층의 노드수)
- 활성화값(마지막 출력값)이 적절히 분포하게 됨

#### He 초깂값 (활성화함수 : relu)
- 표준편차가 $\sqrt{\frac{2}{n}}$ 인 초기값 (n = 앞 계층의 노드수)
- 활성화값(마지막 출력값)이 적절히 분포하게 됨

**배치정규화**<br>
가중치 초기화 없이 활성화값을 적절히 분포시킬수 있는 방법<br>
Affine이 끝난 행렬를 활성화함수를 거치기 전에 평균이 0, 분산이 1이 되도록 정규화
{: .notice}
---

## 오버피팅
#### 가중치 감소
- 가중치가 W라면 가중치 감소는 $\frac12\lambda W^2$이 된다는데...

#### 드롭아웃
- 다음 계층의 모든 노드로 연결하는 것이 무작위의 몇 개의 노드로만 전달
- 순전파때 통과되지 않은 노드는 역전파때도 통과하지 않음

**앙상블학습**<br>
여러번의 학습을 평균내어 학습하는 모델. 드롭아웃이 앙상블학습과 매우 유사함
{: .notice}

---

## 하이퍼파라메터 최적화
- 10의 계승 단위로 범위를 지정하여 테스트
