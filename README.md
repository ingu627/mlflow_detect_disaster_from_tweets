## mlflow_detect_disaster_from_tweets

- **데이터** : [Natural Language Processing with Disaster Tweets - Kaggle](https://www.kaggle.com/competitions/nlp-getting-started/data)
  - 주어진 트윗이 실제 재난에 관한 것인지 아닌지를 예측하기
  - 즉, 실제 재해에 대한 트윗과 그렇지 않은 트윗을 예측하는 기계 학습 모델을 구축
- **자연어 처리 코드 참조** : [Detecting Disaster from Tweets (Classical ML and LSTM Approach) - Mazi Boustani](https://towardsdatascience.com/detecting-disaster-from-tweets-classical-ml-and-lstm-approach-4566871af5f7)
  - **LSTM** : 장기 의존성을 학습할 수 있는 일종의 RNN(Recurrent Neural Network)으로 내부 메모리 시스템으로 설계하면서 정보를 장기간 기억할 수 있다.
  - **RNN** : 입력과 출력을 시퀀스 단위로 처리하는 시퀀스(Sequence) 모델
  - **GloVe embedding** :  카운트 기반과 예측 기반을 모두 사용하는 단어 임베딩 방법론
- **MLOps 툴 참조 : MLflow** : [mlflow.org - official site](https://mlflow.org/) 
  - **MLflow** : 머신러닝(Machine learning) 모델의 실험을 tracking하고 model을 공유 및 deploy 할 수 있도록 지원하는 라이브러리

<br>

### 환경

- **OS** : Ubuntu 20.04.1 LTS
- **CPU** : Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz
- **RAM** : 32GiB
- **GPU** : NVIDIA Corporation TU104 [GeForce RTX 2080]
- **Python** : 3.8
  - **CUDA** : 11.3
  - **CuDnn** : 8.2.1
  - **Tensorflow-gpu** : 2.8.0
  - **MLflow** : 1.24.0

<br>

### 각 폴더 의미

- **data** : 각 데이터
- **etc(preprocess)** : 데이터를 추출하기 위한 코드
- **mlruns/0** : 임의의 mlflow 작업
- **original_code** : 자연어 처리 참조 코드
- **test_env** : 실제 연구를 위한 test 폴더
- **detect_disaster_from_tweets (file)** : mlflow 작업을 위한 기본 코드



<br>

### 연구 : Resolving Data Drift in Disaster Response Model using MLOps based Adaptation

- **Data Drift** : 데이터 특징, 구조, 의미론 및 인프라에 대한 예기치 않은 변경 사항

<br>

- **실험 조건**
  1. Drift 대응 전략에 따른 정확도와 에포크당 정확도 비교
  2. 재학습 정도에 따른 정확도 비교
  3. 데이터 드리프트 정도에 따른 비교

<br>

- **실험 환경**
  - **target label**
    - **1** : 재난 상황 O
    - **0** : 재난 상황 X

  1. drift 전 데이터 (가정) : 재난O 30%, 재난X 70%
  2. drift 후 데이터 (가정) : 재난O 40%, 재난X 60%
  3. epoch : 50회, epoch of retraining : 20회
  4. batch size : 1024, total batch size : 10000
  5. Learning rate : 0.001, optimizer : Adam, loss : binary_crossentropy
  5. 같은 작업 20회 반복해서 평균 정확도 구하기
  6. test accuracy로 성능 비교

<br>

- **결과**
  - "drift 전 데이터"의 모델 : 78.19% 
  - "drift 전 데이터"의 모델로 "drift 후 데이터" test (재학습 X): 56.47% 
  - "drift 전 데이터"의 모델로 "drift 후 데이터" 재학습(20%) test : 61.11%
  - "drift 전 데이터"의 모델로 "drift 후 데이터" 재학습(40%) test : 69.83%
  - "drift 전 데이터"의 모델로 "drift 후 데이터" 재학습(60%) test : 71.04%
  - "drift 전 데이터"의 모델로 "drift 후 데이터" 재학습(80%) test : 72.06%
  - "drift 전 데이터"의 모델로 "drift 후 데이터" 재학습(100%) test : 71.18%
