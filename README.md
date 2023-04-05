# PSM (Propensity Score Matching)

## **1. 성향점수 분석이란?**
> 성향점수란 연구 대상이 특정 공변량에 의해 대조군이 아닌 실험군에 포함될 확률을 의미하며, 0에서 1사이의 값을 가진다.
> 
> 예를 들어 우울 경험 여부가 의료비 지출에 미치는 영향을 알아보고자 할 때, 우울 경험 이외에도 의료비 지출에 영향을 줄 수 있는 신체적 만성 질환과 같은 특정 공변량들에 의하여 선택편향이 발생할 수 있는 문제점이 발생할 수 있는데, 이런 문제를 해결하기 위해 성향점수 분석을 사용한다. 
> 
> 성향점수는 주로 로지스틱 회귀분석을 사용하여 추정하며, 이외에도 CART나 최근에는 배깅, 부스팅, 랜덤 포레스트, 인공신경망(ANN)등을 사용할 수도 있다.
> 
> 로지스틱 회귀분석을 사용하여 성향점수를 추정 할 때에는, 실험군에 포함되는지를 기준으로 binary 형태로 종속변수를 설정하고, 보정하고자 하는 공변량을 독립변수로 설정한다.
> 
> 이렇게 해서 나온 확률값이 바로 성향점수(Propensity Score)이며, 실험군에 속한 대상자들은 가장 근접한 성향점수 값을 가지고 있는 대조군의 대상자와 짝지어지게 되고 짝을 이루지 못한 대상자들은 분석에서 제외된다.
> 
> 성향점수 짝짓기의 방법에는 최근접 이웃 매칭(Nearest neighbor matching), 최적 쌍 매칭(Optimal pair matching), 최적 완전 매칭(Optimal full matching) 등이 있다. 

## **2. PSM Methods**
> **1. 최근접 이웃 매칭 : nearest neighbor matching**
> - control 유닛과 treated 유닛간의 거리를 산출하고, 이를 기준으로 각 treated에 가장 가까운 control을 선택하여 매칭
> - 각각의 매칭 쌍들은 다른 유닛들이 어떻게 매칭되는지와 상관없이 이루어지므로 최적화가 목적이 아닌 greedy한 방법이다.

> **2. 최적 쌍 매칭 : optimal pair matching**
> - 유사한 성향점수를 가진 대조군과 실험군의 연구대상들을 하나의 계층으로 분류하며, 이렇게 여러 개의 계층으로 나누어지는 과정에서 매칭이 이루어짐
> - 각각의 treated를 하나 이상의 control과 쌍을 이루려고 하는 점에서 nearest와 유사하지만, 전반적인 데이터를 고려하여 최적화하는 매칭을 선택하려고 한다는 점에서 차이가 있음

> **3. 최적 완전 매칭 : optimal full matching**
> - 모든 control과 treated을 매칭하여 남는 연구대상이 없도록 하는 매칭 방법

## **3. R) Matchit 패키지**
> - Rstudio에서는 Matchit 패키지를 사용하여 성향점수 매칭을 할 수 있음
> - 참고 -> [https://github.com/kosukeimai/MatchIt](https://github.com/kosukeimai/MatchIt)
> - summary(matched)의 아웃풋 설명 
> ![image](https://user-images.githubusercontent.com/92166406/230107735-640fa86c-4cf7-40fa-8b76-ebaa533f7f81.png)
