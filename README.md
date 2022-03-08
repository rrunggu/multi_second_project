# Air Bnb 호스트를 위한 가격 예측 모델



### 주제 선정 이유

코로나가 종식되면 가장 하고 싶은 활동이 해외 여행이라는 정보를 통해 코로나 종식 이후 여행 수요자가

많아 질 때 효율적인 숙소 제공을 위해 호스트를 위한 airbnb 가격 예측 모델링 구현



### 프로젝트 개요

뉴욕시의 airbnb 호스트를 위한 숙소 가격을 머신러닝 회귀의 다양한 분석 기법을 알아보고 적용하여 최적의 Rmse 값 도출



### 프로젝트 기간

2021.09.09~2021.09.30



### 프로젝트 진행 과정

(데이터 수집 --> 데이터 전처리 --> 데이터 모델링 --> 결론 )



#### 1. 데이터 수집

- 캐글에서 데이터 수집

  

  ![image](https://user-images.githubusercontent.com/98143525/157173970-ca4dd1f2-f91f-447a-a082-c19b4f6e3401.png)

- 데이터 명세

  ![image](https://user-images.githubusercontent.com/98143525/157174890-8ea3caec-38f5-406a-acb7-3f77d734d1e7.png)

​		- 전처리가 필요한 컬럼 선정 : 

​		**neighborhood_group**, room_type,**price**,**minimum_nights**,reviews_per_month,**availability_365

- 데이터 시각화

  <뉴욕 자치구별 에어비앤비 개수 시각화>

  ![image](https://user-images.githubusercontent.com/98143525/157175106-ef73336d-aeb8-472b-a56e-13f07cd48d01.png)

​		<뉴욕 자치구별 에어비앤비 숙소 유형 시각화>

​		![image](https://user-images.githubusercontent.com/98143525/157175185-79a9b475-786a-407a-bac1-776ed2526bd8.png)

#### 2. 데이터 전처리

- 'price'컬럼에 0 달러 삭제

​	![image](https://user-images.githubusercontent.com/98143525/157175636-8ba3db91-7756-4f90-91e2-ae1d85da8011.png)

- 'mimimum_nights' 이상치 삭제  --> 365일 이상 값 삭제

​	![image](https://user-images.githubusercontent.com/98143525/157175732-9f920c4d-eb96-4d33-9f95-e51b9f3779bb.png)



#### 3. 데이터 모델링

- availability_365 컬럼에 0 값을 평균값, 중위수, 365 세가지로 구분하여 모델링 진행

​	![image](https://user-images.githubusercontent.com/98143525/157176068-bd37f65b-34c1-433d-ab8c-a336b8f6c8b4.png)

​		

- 회귀 기법 중 사용해 볼 수 있는 기법에 전부 적용

​	<선형, 릿지 , 라쏘 회귀>

​	![image](https://user-images.githubusercontent.com/98143525/157177162-53d3738a-6c10-4371-afa6-0b18c7a9d5f3.png)

​	![image](https://user-images.githubusercontent.com/98143525/157177338-bcac315d-626a-4607-9cec-8c003a9b5fa7.png)

​	< 라쏘 모델 개선을 위해  최적의 alpha 값 모델에 대입 >

![image](https://user-images.githubusercontent.com/98143525/157177660-b2386bb9-7681-442d-93dc-bbd01156e33b.png)



![image](https://user-images.githubusercontent.com/98143525/157177738-761f5a7e-cc5e-4a97-bb9f-dbd08a731ade.png)



​	< 다양한 기법을 활용한 모델링 결과>

​	![image](https://user-images.githubusercontent.com/98143525/157178053-4550b22a-f222-48d7-96d3-7064b43b22b7.png)



#### 4. 결론 

- availability_365 의 0 값 --> 중위수 대체가 가장 효율적
- 분리 비율이 8:2 , 스태킹 모델을 적용했을 때 가장 좋은 성능을 가진다
- 스태킹 모델을 적용해 호스트가 숙소를 추가할때 가격을 예측 할 수 있는 서비스를 구현
