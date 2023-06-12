# 🎬영화관객수예측🎬

## 데이터


- train.csv
- test.csv
- submission.csv

---
#### Column
- title : 영화의 제목
- distributor : 배급사
- genre : 장르
- release_time : 개봉일
- time : 상영시간(분)
- screening_rat : 상영등급
- director : 감독이름
- dir_prev_bfnum : 해당 감독이 이 영화를 만들기 전 제작에 참여한 영화에서의 평균 관객수(단 관객수가 알려지지 않은 영화 제외)
- dir_prev_num : 해당 감독이 이 영화를 만들기 전 제작에 참여한 영화의 개수(단 관객수가 알려지지 않은 영화 제외)
- num_staff : 스텝수
- num_actor : 주연배우수
- box_off_num : 관객수

##### box_off_num :예측피처
---

### 장르별 관객수 막대그래프
![image](https://github.com/overthemoonlala/movie/assets/99886389/4a0cae86-b9aa-428d-aa7f-c938ec7df292)

드라마/코미디/느와르/액션 순으로 관객 수가 높다

### 히스토그램으로 변수 분포 확인

![image](https://github.com/overthemoonlala/movie/assets/99886389/46d9c5fe-a839-4b10-ac9b-d4fc0ed311d1)

### 상관분석
	time	dir_prev_num	num_staff	num_actor	box_off_num
time   	1.000000	0.306727	0.623205	0.114153	0.441452
dir_prev_num	0.306727	1.000000	0.450706	0.014006	0.259674
num_staff	0.623205	0.450706	1.000000	0.077871	0.544265
num_actor	0.114153	0.014006	0.077871	1.000000	0.111179
box_off_num	0.441452	0.259674	0.544265	0.111179	1.000000

![image](https://github.com/overthemoonlala/movie/assets/99886389/4d71254e-fa59-4ed6-8914-f6cc68ab496e)
---
## 각각의 변수로 살펴보기

### distributor 배급사
배급사는 169개가 있으므로, title과 달리 배급사와 영화는 일대다 관계
- 과거 배급 영화 수가 배급사의 파워(순위)를 결정하는 요소일 수 있다.
- 과거 많은 관객을 모은 배급사일수록 향후에도 많은 관객을 모을 것으로 기대할 수 있다.

배급사별 영화 수 확인
![image](https://github.com/overthemoonlala/movie/assets/99886389/4041982c-80f6-444f-ad4c-19e1950b741d)

배급사별 관객 수 확인
![image](https://github.com/overthemoonlala/movie/assets/99886389/0df7a973-f999-4086-ac2c-3ee176bbeba2)

### release_time 개봉일
영화 흥행에 개봉 일정이 어떤 영향을 미치는지 알아보기
![image](https://github.com/overthemoonlala/movie/assets/99886389/9ce1b220-d48a-4775-aaa1-18d41df40d13)
한눈에 보기 불편한 관계로 년도별로 끊어서 보기

![image](https://github.com/overthemoonlala/movie/assets/99886389/964f4140-5e69-446a-9365-e9946f940bdd)
2013년에 정점을 찍고 2014년부터 감소하는 추세이다.
수~목요일에 영화가 개봉하므로 가장 관객수가 많다.

![image](https://github.com/overthemoonlala/movie/assets/99886389/3679305b-bd4f-400f-84e2-5285771bf749)
년도별/월별로 나눈 그래프


![image](https://github.com/overthemoonlala/movie/assets/99886389/aa308e02-7bae-4f66-9153-4c4afd5a22c5)
년도별 그래프 합하기
12월-1월, 7-8월에 높은 것으로 나타난다


### time 시간
![image](https://github.com/overthemoonlala/movie/assets/99886389/1d1e1af4-18fd-48c3-a093-4be9d440e35a)
120-140분 사이의 영화가 많은 관객수를 차지한다.



### screening_rat 상영등급
![image](https://github.com/overthemoonlala/movie/assets/99886389/1d00f4ce-aab2-4bf9-ba03-1dea6f55904a)


### director, dir_prev_bfnum, dir_prev_num
- director: 감독 이름
- dir_prev_bfnum: 해당 감독이 이 영화를 만들기 전 제작에 참여한 영화에서의 평균 관객수 (단 관객수가 알려지지 않은 영화 제외)
- dir_prev_num: 해당 감독이 이 영화를 만들기 전 제작에 참여한 영화의 개수 (단 관객수가 알려지지 않은 영화 제외)

![image](https://github.com/overthemoonlala/movie/assets/99886389/cbf73c2a-85a6-4000-bcbc-6a3025a82b0b)
![image](https://github.com/overthemoonlala/movie/assets/99886389/3836cdeb-efc1-4adf-b0e9-01a9bb7c4a17)

- null값인 데이터의 dir_prev_num, 즉 이전에 참여한 영화의 갯수가 0인 것을 알 수 있다.
- 일반적으로 측정되거나 조사된 값에서 55%가 비어 있다면 유의미한 데이터라고 보기는 어려울 수 있다.
- 하지만, 해당 변수는 감독이 영화를 만들기 전 제작에 참여한 영화에서의 평균 관객수로, 이전에 영화 제작에 참여하지 않은 신인 감독의 경우 0이 나오게 될 수도 있다.
- 적절히 구간을 나누어 변수로 만들어보자.

![image](https://github.com/overthemoonlala/movie/assets/99886389/75df0dad-4fe9-410a-9c74-715a39e3dab1)
![image](https://github.com/overthemoonlala/movie/assets/99886389/31c396fa-7fdb-4e1e-9816-0afaab995c70)
![image](https://github.com/overthemoonlala/movie/assets/99886389/68443b05-115e-447a-bc46-bcf8c0d2f8f7)

-이렇게 구분하는 경우 train 데이터에서는 잘 구분될 수 있지만 새로운 데이터에서는 의미가 없을 수 있다.
-거장 감독이지만 train set에 없다면 새로운 데이터를 검증하기 어려우며, 신인 감독인 경우에도 마찬가지일 수 있다.

### num_staff 스태프 수
- 스태프 수가 많을수록 제작비가 많이 들어갔다는 의미이니, 관객을 많이 모을 수 있을까?
![image](https://github.com/overthemoonlala/movie/assets/99886389/e2608c31-c65e-4de2-abe2-be338f2144ea)


### 원핫인코딩
![image](https://github.com/overthemoonlala/movie/assets/99886389/b399f350-3ee9-4785-84b7-6b0fa18a1e65)


### Modeling - Prediction - Submission
![image](https://github.com/overthemoonlala/movie/assets/99886389/32975664-2b25-412f-b54f-f2b6bce24e8b)
![image](https://github.com/overthemoonlala/movie/assets/99886389/86f4495d-7f8a-4f7f-9808-67f86b2743b7)
![image](https://github.com/overthemoonlala/movie/assets/99886389/056f0232-67ed-4aad-b7fa-3f2e1af5deca)
![image](https://github.com/overthemoonlala/movie/assets/99886389/6a425368-d19a-4f11-a6d4-559f6c44029a)
![image](https://github.com/overthemoonlala/movie/assets/99886389/29ce2417-db82-4659-827a-ae641bc59c1b)



