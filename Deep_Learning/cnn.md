> 참고 https://halfundecided.medium.com/%EB%94%A5%EB%9F%AC%EB%8B%9D-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-cnn-convolutional-neural-networks-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-836869f88375

> 참고 https://halfundecided.medium.com/%EB%94%A5%EB%9F%AC%EB%8B%9D-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-python-keras%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4-%EC%86%90%EA%B8%80%EC%94%A8-%EC%88%AB%EC%9E%90-%EC%9D%B4%EB%AF%B8%EC%A7%80%EB%A5%BC-%EC%9D%B8%EC%8B%9D%ED%95%98%EB%8A%94-cnn-convolutional-neural-networks-%EB%AA%A8%EB%8D%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-2c7c315e9958

# CNN 주요 개념

## CNN 이란? 

Convolutional Neural Networks의 약자로 딥러닝에서 주로 이미지나 영상 데이터를 처리할 때 쓰인다. 

이미지 전체보다는 부분을, 그리고 이미지의 한 픽셀과 주변 픽셀들의 연관성을 살림으로써 공간적/지역적 정보가 손실되는 DNN의 문제점을 해결한 모델이다.

## Convolution

CNN에 넣어줄 입력값은 matrix로 표현된 이미지이다.

![1](https://miro.medium.com/max/875/1*xVKN9dBAzPn7E-DwaIjK3Q.png)

![2](https://miro.medium.com/max/875/1*s6yBccVNHVuEEO9Ur6Az9w.png)

만약 Input이 5x5 matrix로 표현된 이미지라면 CNN에는 필터(커널)이 존재한다. 

위의 예시로는 3x3 크기의 필터이다. Convolution은 이 하나의 필터를 입력값 이미지의 모든 영역에 반복 적용해 패턴을 찾아 처리하는 과정이다. 그 과정에서 matrix와 matrix 간의 Inner Product 연산처리가 일어난다.

이러한 연산을 전체 이미지 matrix에 필터 matrix를 조금씩 움직이며 반복하여 그 계산값이 모인 matrix(사진의 분홍색 행렬)를 결과값으로 얻는다.

### Inner Product

![Inner Product](https://miro.medium.com/max/875/1*Gj7y0S1VG35njLYk4Vy_0A.png)

같은 크기의 두 matrix에서 각 위치에 있는 숫자를 곱해 모두 더해주는 연산이다.

## Zero Padding

Convolution 처리를 하여 결과값의 크기가 줄어들어 손실되는 부분이 발생하는 것을 막기 위해 Padding을 적용해주는 것이 좋다.

Zero Padding이란 matrix의 크기를 늘린 후 비어있는 곳을 0값으로 채우는 처리이다. 이렇게 하면 Convolution 과정에서 입력값의 크기와 결과값의 크기가 같아지므로 손실이 없어진다.

## Stride

Stride는 필터를 얼마만큼 움직여 주는가에 대한 값이다. 

예를 들어 stride 값이 1일 경우 필터를 한칸씩 움직여서 이미지의 모든 영역을 연산처리 한다. stride의 default 값은 보통 1이다.

## The Order-3 Tensor

![The Order-3 Tensor](https://miro.medium.com/max/753/1*1PEUso2BlIvWkLZXtQeurA.png)

보통 이미지는 2차원이기에 2차원 행렬로 연산을 수행한다고 생각하지만, 입력값이 3차원인 경우도 존재한다. 

예를들어 색은 R, G, B 의 세가지 채널로 표현하기 때문에 채널의 수를 포함하여 삼차원의 크기로 표현할 수 있다. 

만약 이미지가 흑백이라면 채널의 수는 1이다. 이러한 모양을 order-3 텐서라고 한다.

# CNN 네트워크 구조

![1](https://miro.medium.com/max/800/1*usA-K08Tn5i6P7eLvV8htg.png)

CNN 네트워크 구조는 기존의 완전연결계층(Fully-Connected Layer)과는 다르게 Convolutional Layer과 Pooling Layer들을 활성화 함수 앞뒤에 배치하여 만들어진다.

## Convolutional Layer

![Convolutional Layer](https://miro.medium.com/max/875/1*E-5sL3jJMIygx0Xm9_y6Ew.png)

입력값에 n개의 필터(위 사진에서는 10개)로 Convolution 처리를 하고, 그 결과값에 활성화 함수(Activation function)를 적용하는 층이다. 

즉 한 Convolutional Layer에서는 Convolution 처리와 Activation function을 적용하는 과정을 수행한다.

### 활성화 함수 (Activation function)

![뉴런](https://miro.medium.com/max/875/1*ms8UwpZicqJ4IGE5tkH06w.png)

선형함수(linear function)인 convolution에 비선형성(nonlinearity)를 추가하기 위해 사용한다. 활성화 함수가 없으면 가중치와 편향은 단순히 선형 변환을 수행하므로 복작한 mapping을 학습할 수 없다. 활성화 함수가 없는 신경망은 선형 회귀 모델일 뿐이다.

주로 사용하는 활성화 함수에는 ReLU와 Softmax(주로 출력에 사용)가 있다.

> 참고 https://medium.com/@snaily16/what-why-and-which-activation-functions-b2bf748c0441

## Pooling Layer

![Pooling Layer](https://miro.medium.com/max/875/1*wGrlfRciYNcqhGqBWSiErg.png)

Pooling이란 각 결과값(feature map)의 크기(dimentionality)를 축소하는 과정이다. 

Convolution 과정을 통해 많은 수의 결과값이 생성 되었는데 이 중에서 correlation이 낮은 부분을 삭제하여 각 결과값의 dimension을 줄인다.

Pooling Layer는 이러한 Pooling을 과정을 수행하는 층이다.

![Pooling](https://miro.medium.com/max/645/1*8DRW7Uw6lHfAdPdXrHiY9w.png)

Pooling에는 대표적으로 크기가 가장 큰 값을 선택하는 Max Pooling과 평균값을 구하여 저장하는 Average pooling이 있다.

## Flatten(Vectorization)

![Flatten](https://miro.medium.com/max/875/1*v8TDECzNYJBrsSvlSLTcNg.png)

위 과정에서 설명한 Convolutional Layer와 Pooling Layer를 번갈아가며 2번씩 수행하고 난 후 Flatten 과정을 처리해준다. 

Flatten (또는 Vectorization 라고도 한다)은 다차원의 텐서를 1차원의 벡터(세로줄로 일렬)로 변환해주는 과정이다. 예를 들어 4x4x20의 텐서는 320-dimension의 벡터로 변환된다.

이미 앞의 과정에서 layer를 거쳐 데이터에 초기 입력값에 대한 공간적/지역적 정보가 담겨졌으므로 1차원 벡터로 변형시켜도 이러한 정보가 사라지지 않는다.

## Fully-Connected Layer(Dense Layer)

![Fully-Connected Layer](https://miro.medium.com/max/875/1*EcOvxbhodURWEjXXepKYIw.png)

완전 연결 계층(Fully-Connected Layer)은 1차원 벡터 형태로 평탄화된 행렬을 통해 이미지를 분류하는데 사용되는 계층이다. '완전 연결 되었다'라는 뜻은 한 층(layer)의 모든 뉴런이 그 다음 층(layer)의 모든 뉴런과 연결된 상태를 뜻한다.

즉 Fully-Connected Layer는 Flatten 처리, ReLU 함수로 뉴런 활성화, softmax 함수로 이미지를 분류하는 과정으로 이루어져있다.

![Fully-Connected Layer](https://blog.kakaocdn.net/dn/bEfepF/btqD7H2rJws/G1plKbDz6FLYNHrkkUFLe1/img.png)

> 이미지 출처와 참고 https://dsbook.tistory.com/59
