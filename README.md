<!-- # CONVOLUTION NEURON NETWARK  -->

# CNN 정리

### CNN?
 `Convolution Layer`를 딥러닝에 추가한 형태로 시신경과 유사한 형태라고 인터넷에 명명 되었으며 실제로는 <br> `Convolution(합성곱)`, `Pooling` 연산을 딥러닝에 추가 함으로써 이미지의 특성을 추출 및 학습 하여 각 클래스를 예측할수 있도록 만든 neural network입니다.

### 학습시에 Accuracy값의 신뢰성

CNN 모델 학습시 accuracy 값이 1.00을 찍는 경우를 많이 보게 됩니다.이러한 이유로는 CNN의 학습데이터셋을 `단순 기억하는 것(과적합:Overfitting)`으로 실제 성능 정확도로 봐서는 안됩니다. <br>
이를 해결하는 방법은 `Dropout Layer`의 활용과 `데이터셋의 재분류` 및 `중복 제거`, `추가데이터 수집`등의 방법이 있습니다. <br>
또한 평가 지표를 `Accuracy` 보다는 `validation accuracy(검증 정확도)`를 활용하는 것으로 모델의 학습 신뢰성을 확인할수 있습니다.
![](https://user-images.githubusercontent.com/132330370/242189569-0050725c-d72d-4b67-901f-f5c579c04744.png)
``` java
 Models.fit(np.array(x),np.array(y),55, 500, validation_split=0.25)
```
### Loss funtion 
`Binary Crossentropy Loss` : 이진 분류 문제에 사용. 출력이 두개의 클래스중 하나일 경우에 사용됩니다. `Best`
<br>
<br>

`Categorical Crossentropy Loss` : 다중 클래스 분류 문제에서 사용. 각 클래스의 확률 분포와 실제 클래스의 원-핫 인코딩을 비교하여 손실을 계산합니다. `Best`
<br>
<br>

`Sparse Categorical Crossentropy Loss` : 다중 클래스 분류 문제에서 사용. 클래스의 인덱스와 실제 클래스의 인덱스를 비교하여 손실을 계산합니다.
<br>
<br>

`Mean Squared Error` : 회귀 문제에서 사용. 예측 값과 실제 값 사이의 평균 제곱 오차를 계산하여 손실을 구합니다. `Best`
<br>
<br>

`Huber Loss` : 회귀 문제에서 사용. 이상치에 민감하지 않은 로스 함수입니다. MSE와 절댓값 손실의 절충 버전입니다.
<br>
<br>

`Dice Loss` : 이미지 분할 문제에서 사용. 예측된 마스크와 실제 마스크의 유사도를 측정합니다.

## Unet
Unet은 `Image Segmentation` 작업에 널리 쓰이는 딥러닝 아키텍처 입니다.<br>
Image Segmentation은 이미지를 픽셀 단위로 분류하여 각 픽셀이 어떤 객체 또는 배경에 속하는지를 결정하는 작업입니다. <br>
Unet은 주로 의료분야에 사용이 됩니다. (X-ray, CT, MRI Image속 암 찾기)

### 구조
![](https://user-images.githubusercontent.com/132330370/242170508-1fb9c8cf-d27c-4135-a4d6-f933dc0778eb.png)

구조는 이름과 같이 U 형태를 지니고 있습니다. 이유를 보면 각 Convolution 레이어들의 사이를 지나는 선이 있습니다. <br>
이 선은 DownScaling의 데이터가 중심 기준으로 반전되는 UpScaling의 같은 높이의 레이어어의 convT를 진 데이터와 4차원 축으로 붙인 다음 다시 Conv 레이어를 지나는 구조로 구성됩니다.
<!-- 이를 다시 풀어 보면 Detector, nn 없는 GAN 과 비슷하다. -->
