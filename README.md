# 2021-AI-project

## Introduction - 실험 요약
이번 실험에서는 Titanic 승선객 데이터셋을 활용한 생존여부 분류기 모델(Titanic Survivor Classifier)을 만들고자 한다. 데이터셋의 경우 Kaggle에서 제공되는 Titanic 승선객 레이블 데이터를 활용하여 Supervised Learning 실험을 진행할 것이다. 데이터셋의 경우 실험 자료로 제공되는 전처리된 데이터를 활용할 예정이기에 추가적인 전처리나 Feature Engineering 없이 실험을 진행할 예정이다.

Label:y의 경우 `Survived`, 즉 생존 여부를 묻는다. 1의 값은 생존, 0의 값은 생존하지 못하였다는 의미를 가진다. 나머지 7개의 Feature를 통하여 `Survived`라는 Categorical data를 예측할 수 있는 분류기(Classifier)를 생성하기 위하여 다음과 같은 일련의 과정을 거쳤다.

우선, EDA를 통해 데이터셋의 모양과 각 Feature가 가지는 의미를 파악하였다. 데이터셋의 경우 전체 데이터의 20%를 Test Set으로 사용하였고, 80%의 경우 Cross-validation 방식을 이용하여 Train Set과 Validation Set으로 사용하였다.

그 후 `Decision Tree`, `Logistic Regression`, `Multilayer Perceptron(MLP)`의 세 모델을 가지고 5-fold Cross-validation을 통해 각 모델들에 대한 최적의 Parameter를 선정하였다. 모델마다 3개의 Parameter를 조작하였고, 평가지표로 `ROC_AUC Score`를 사용하였다. 비교에 있어서는 많은 Parameter를 제한된 자원을 활용하여 최대한 많이 비교할 수 있도록 Loop Iteration을 활용하였다.

각 모델별로 최적의 Parameter를 구한 뒤, 해당 모델들을 Train Set에 학습시켜 최종 모델을 생성하였다. 학습된 최종 모델을 Test Set에 적용하여 나온 결과를 비교 분석하였고, 이 역시 `ROC_AUC Score`를 최종 평가지표로 사용하였다.

그 결과 `Multilayer Perceptron(MLP)`이 가장 높은 성능을 가져오는 것으로 확인되었다. 이 모델의 Parameter는 다음과 같다.

`MLPClassifier(hidden_layer_sizes=(150,), activation='logistic', solver='adam', max_iter=10000, random_state=42)`

해당 모델은 다음과 같은 성능을 가져왔다.

`Accuracy = 0.79, Precision = 0.75, Recall = 0.70, F1-score = 0.72, ROC AUC Score = 0.77`

최종적으로, Titanic 승선객 생존여부 분류기에 사용할 모델로 **MLP**를 선정하였다.

