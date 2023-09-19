<div>2023 제 3회 코피스빅데이터 컨퍼런스 최종본선(Top10) 진출 작품</div>
<div fontsize="5px">※ 대회정책상 코드공유는 따로하지 않았습니다.</div>

<div>
  <h1>🎖️ 2023 제3회 코피스빅데이터 컨퍼런스<br><br>
   📈 위드코로나 시대 공연시설 유형별 회복탄력성 분석</h1>
</div>
<h4> 💭 Language : Python, QGIS <br><br>
     📝 Library : Pandas, Numpy, Matplotlib, Seaborn, Haversine, Geopandas, Scikit-learn <br><br>
     🛠  Tool : Jupyter <br><br>
     📅 진행기간 : 2023.06.23 ~ 2022.09.08</h4><br>

### 👨‍👦‍👦 팀원소개
<table>
<tbody>
  <tr>
    <td align="center"><img src="" width="20px;" alt=""><br /><b>팀장 : 오지현</b></a><br /></td>
    <td align="center"><img src="" width="20px;" alt=""/><br /><b>팀원 : 유제우</b></a><br /></td>
    <td align="center"><img src="" width="20px;" alt=""/><br /><b>팀원 : 임승재</b></a><br /></td>
   <tr/>
</tbody>
</table>
<br>
<h3><img width="1062" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/809be072-33cd-4aba-a3e9-d01e9fead33a"></h3>

# 💡 분석 배경 및 필요성
* 수도권 공연시장의 회복세는 팬데믹 이후 꾸준히 상승<br>
* 수도권과 비수도권과의 문화 격차는 더욱 악화<br>
* 비수도권 내에서도 지역별 공연시장 회복 정도의 확연한 차이가 존재<br>
* 대극장과 소극장의 경우 팬데믹 전후 공연매출에 큰 차이가 없었지만 중극장의 경우 매출이 하락세임<br>
* 이를 통해 분석 대상을 비수도권의 중극장으로 확정시켰고, 회복탄력성을 구하기 위하여 충격지점을 '제 1차 집합금지'시점인 2020년 3월로 지정
* 해당 충격지점을 기준으로 극장별 매출에 얼마나 손해가 생겼는지, 기대매출로 얼마나 빠르게 회복하였는지의 지표인 '회복탄력성'지수를 도출하여 분석할 것을 기획
<br>

# 🔎 데이터 전처리
## 1) 데이터 제거
* 수도권과 제주도 지역 공연시설 제거
* 300석 이상 1000석 미만인 중극장외 공연시설 제거
* '할인종류'와 '결제수단'이 모두 불명확한 경우는 이상치로 판단하여 제거
* 입장권고유번호에서 중복데이터가 존재할 경우 1개를 제외한 데이터 제거

## 2) 데이터 수정
* 할인금액이 0원이지만, 실제 예매금액과 티켓가격이 일치한 경우, 예매금액과 장당금액 수정
* '할인금액'이 0원이지만, '예매/취소금액', '장당금액'이 일치하는 경우 장당금액 수정
* 예매/취소금액이 0원이고, 장당금액보가 할인금액이 큰 경우 제거
* 예매/취소금액이 0원이고, 장당금액 > 할인금액인 경우 예매금액으로 대체
* 예매/취소금액, 할인금액, 장당금액 모두 0원인 경우 같은 공연시설의 같은 공연 데이터의 평균값으로 대체<br><br><br>

## 3) 회복탄력성 지수 계산용 데이터 구축
<img width="846" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/881589ce-b148-469c-932e-670f892ebe20">
* 매출의 최소지점을 파악할 수 없는 2,3번의 경우 제거를 하였고 최종적으로 138개의 중극장으로 추릴 수 있었음
<br><br><br>

## 4) 요인회전 및 요인점수 계산
* PCA를 통해 요인을 도출했기 때문에, 요인끼리의 상관성이 없었음. 따라서 직교회전의 Varimax를 적용
* 위에서 도출한 요인 적재값을 가중치로 사용하여 요인점수 도출
* <요인별 요인점수 계산식>
<img width="530" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/d8b54c97-24a6-44d5-860c-4bad05c01e66">
<br><br><br>

<br><br>

# 📊 공연시설 유형 분류
## 1) 공연시설별 지표 생성
<h3><img width="972" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/347f08f2-46b1-4661-aefe-4129da9d6171">
</h3>
* 공연수요에 영향을 미치는 객곽적인 지표 확인을 위하여 관련 논문 참고후 최종변수 선정

* 지역의 규모, 경제수준, 접근성, 문화수준을 대표할 수 있는 총 15개의 지표 생성

## 2) KMO검정과 Bartlett구형성 검정
* 변수 후보군이 요인 분석 혹은 주성분 분석에 적합한지 판단하는 통계적 절차
* 먼저 변수들 간의 척도 차이를 해소하기 위하여 표준화작업 진행
* KMO검정 실시 결과, 0.77로 상당히 적합한 변수로 구성된 것 확인
* Bartlett검정 실시 결과, p_value값이 거의 0으로 적합한 것 확인

## 3) Factor Analysis
<h3><img width="553" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/d12aa506-c1bf-4070-ad1c-f55311be9ddf">
</h3><br>
* Scree Plot을 활용하여 고유값이 1보다 크면서 해석 가능한 수준인 3개의 요인 추출

* 요인 적재값 도출을 통한 각 요인별 특징 도출

* 이때, 요인분석 결과에 대한 신뢰성 검증을 위해 Tucker Lewis's reliability를 사용하였고, 해당값이 0.6 이상으로 도출되어 적합한 것으로 확인

## 4) 요인회전 및 요인점수 계산
* PCA를 통하여 변수의 축을 최소화하였고, 이를 통해 요인적재값을 도출하였기 때문에 요인별 상관성은 없는것으로 나타남
* 따라서 직교회전의 Varimax를 적용하였음
* 그 후, 요인점수 도출에 요인 적재값을 가중치로 사용하여 요인점수를 계산함<br>
요인점수 계산식
<h3 align="center"><img width="530" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/c409db83-5fc1-4085-8642-2a9265ecf9bf"></h3>


## 5) 공연시설 군집분석
<h3 align="center"><img width="994" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/f90d89f2-590c-4af9-92a9-2fdd2c05a810"></h3>
* 클러스터링 대상 변수를 위에서 도출한 공연시설별 요인점수로 지정함

* 군집분석의 결과향상을 위하여 요인점수의 비대칭성 보완을 위하여 로그변환후 정규분포로 수정함

* Kmeans++ 군집분석 기법을 이용하여 극장을 유형화 하였으며, 군집분석의 결과확인을 위하여 실루엣계수와 군집의 너비를 모두 고려하여 최적의 K선정함

<br><br>
# 📄 Modeling
## 1) K-means clustering
<h3 align="center"><img src= https://github.com/LHG-Git/project/assets/100845169/72117835-2fb5-451f-a343-3c49078b02ae></h3>

* <strong>Group0</strong>은 시간과 관계없이 승하차 분포가 고르기 때문에 <strong>상업그룹</strong><br> 
* <strong>Group1</strong>은 오전에는 승차에, 오후에는 하차에 분포가 되어 있기 때문에 <strong>주거그룹</strong><br>
* <strong>Group2</strong>는 오전에는 하차에, 오후에는 승차에 분포가 되어 있기 때문에 <strong>업무그룹</strong><br><br>

#### EDA과정에서 업무지역과 주거지역은 출퇴근 시간에 유동인구가 밀집되어 있다는 근거를 통해, <strong>Group1과 Group2를 통합</strong><br>
#### <strong>클러스터링 기법을 통해 최종적으로 Group0(상업 그룹)과 Group1(업무주거 그룹)으로 분류</strong><br><br><br>

## 2) ANOVA검정
* EDA 및 분석을 통해 사용하고자 하는 변수가 승하차 인원 값에 미치는 영향이 <strong>통계적으로 유의한지 확인하기 위해 진행</strong><br><br><br>


## 3) 변수선정
|변수선정|변수|
|:------:|---|
|공통변수|노선명, 버스정류장 개수, 노선수, 계절, 기온, 공원 개수, 요일, 휴일여부, 누적휴일, 1일우량, 량|
|상업그룹 변수|산업, 숙박/음식, 레저/관광/예술, 영화관 개수, 백화점 개수|
|업무주거그룹 변수|행정, 대학생 수, 학생 수(중,고등), 교육/보건, 중소기업 개수|<br><br>
<br>


## 4) Hold-Out 검정
* <strong>Lidge, Lasso, RandomForest, Xgboost, DecisionTree, LightGBM</strong> 등 여러 회귀분석 모델들 중 모델 선정을 위한 <strong>Hold-Out 검정</strong>을 진행<br>
* 그 결과, <strong>9호선 신설역 수요 예측에 LightGBM 모델이 가장 적합할 것이라 판단하여 진행</strong><br><br><br>

## 5) LightGBM
#### <strong>LightGBM 모델을 통한 승하차수 예측</strong>,<strong>평균 절대 오차값인 MAE값을 통한 모델 성능 검증</strong><br><br>
<h3 align="center"><img src="https://github.com/LHG-Git/project/assets/100845169/2346017d-3083-46b1-828b-ba5be613f923" width = 500px height = 300px></h3>

#### (1차) : 파라미터 조정 및 k-fold 교차검증을 이용하지 않고, LightGBM 모델의 default값 그대로 초기 예측을 진행 

* <strong>상업그룹의 MAE : 2600명, 업무주거그룹의 MAE값 : 2100명</strong><br><br>
<h3 align="center"><img src="https://github.com/LHG-Git/project/assets/100845169/8c5522d5-9b82-4be0-a05c-faaa40cb8710" width = 500px height = 300px></h3>

#### (2차) : 하이퍼 파라미터 튜닝을 통해 최적의 파라미터 값을 지정 및 5차 k-fold를 이용하여 노이즈 값을 최소화한 후 예측을 진행


* <strong>상업그룹의 MAE값이 1500명, 업무주거그룹의 MAE값 990명<br>
  
### 결론 : 오차 값이 1000~1100명 정도 감소하여 성능이 향상 👍<br><br>
<br>

## 6) 모델 성능 향상
* 최적의 하이퍼 파라미터 값을 이용하기 위해, <strong>하이퍼파라미터 튜닝</strong> 진행<br><br>
* 노이즈 값을 없애고자, <strong>K-Fold 교차 검증</strong> 진행<br><br>
<br>

# 💻 예측결과
### 1) 역별 예측 결과
<h3 align="left"><img src="https://github.com/LHG-Git/project/assets/100845169/369cd3a7-8618-42a7-ad4d-cf3150945743" width = 1000px height = 400px></h3>

* 현재 9호선 역별 일평균 수요 승객은 2.7만명
* 길동생태공원, 명일공원역은 비교적 원활
* 샘터공원역은 9호선 일평균 수치와 비슷
* 고덕역은 다양한 인프라가 형성되어 있어 약 3.8만명으로 1일 승하차 평균을 크게 넘어 유동인구 혼잡 예상<br><br>

### 2) 혼잡률
<h3 align="center"><img src="https://github.com/LHG-Git/project/assets/100845169/ba09e4e5-8643-4570-8c1a-4fe10b46bd82" width = 500px height = 300px></h3>

* 고덕역 예측 수요 약 3.8만명
* 고덕역 혼잡률 200% 이상  
* 고덕역의 승하차 수요와 현재 환승역임을 감안하여 급행역으로 선정<br><br>

# 📍 9호선 신설역 그룹화
### 1) 업무주거 그룹 : 길동생태공원, 명일공원역, 고덕역
* <strong>길동생태공원</strong>의 경우 시점역, 천호대로와 동남부 교차로 및 주변의 공원과 더불어 아파트가 밀집<br><br>
* <strong>명일공원역</strong>의 경우 중,고등학교 등 각종 교육시설과 일반 주택 및 아파트가 밀집<br><br> 
* <strong>고덕역</strong>의 경우 고등학교, 병원, 아파트 등 각종 교육 시설이 밀집<br><br> 
* <strong>따라서 길동생태공원, 명일공원역, 고덕역은 업무주거 그룹에 해당</strong><br><br>

### 2) 상업그룹 : 샘터공원역
* <strong>샘터공원역</strong>의 경우엔 고덕 강일 공공주택 1지구가 위치해있고, 고덕비즈밸리 중심 상업지역에 위치<br><br> 
* <strong>따라서 샘터공원역은 상업그룹에 해당</strong><br><br>

# 🚩 정책 제안
### 1) 대각선 신호등 설치
* 대각선 신호등을 설치하지 않으면 유동인구가 많은 지하철역에서 사람들이 몰리는 현상이 발생할 것
* 그러면 공간부족으로 차도에 발을 딛는 사람들이 점점 늘어날 것이고 그들의 안전은 보장할 수 없음 
* 그렇기 때문에 다른 역에 비해 수요승객수가 가장 많은 고덕역의 경우, <strong>사람들이 원활하게 이동할 수 있는 대각선 신호등 배치를 한다면 교통 및 혼잡한 상황을 예방할 수 있을 것으로 예상됨</strong>

### 2) 급행역 선정
* 승하차 수요는 중요한 고려사항이며 고덕역의 경우 환승노선이 2개인 점과, 예측승객수가 3만 명을 넘는 것을 감안했을 때, <strong>급행역으로 선정이 되는 것이 9호선 내부의 혼잡도를 예방할 수 있는 방안임</strong>

### 3) 도심 공동화 예방
* 도시가 성장하면서 땅값이 오르고, 그로인해 상업 시설들이 다수를 차지하게 됨
* 상업 시설의 특성상 상주인구는 매우 적은 대신 유동 인구가 많은 편
* 결국, 도심의 상주인구는 줄어들게 되는데, 이를 예방하기 위해 <strong>상업그룹에 해당하는 고덕역과 샘터 공원역 주변에 신축되는 고층건물에 대해서는 일정비용을 주거 용도로 하여 직장과 주거지가 이웃하도록 짓는다면, 도심공동화 현상을 예방할 수 있을 것으로 예상됨</strong>

### 4) 8량 추진화
* 9호선의 수요승객이 하루 평균 69만 명에서 약 78만 명으로 늘어남 
* 9호선의 지하 박스 구조물 자체는 8량 길이에 맞추어져 있어 신호, 전기, 승강장, 마감, 조명 등 공사를 진행 할 경우 막대한 예산이 들어감
* 9호선 승강장은 최대 8량까지 운행할 수 있도록 설계됐지만 제대로 활용하지 못하고 있음
* 위 예측결과는 9호선 8량화 추진에 힘을 실어줄 수 있는 근거로 활용될 수 있음

### 5) 적절한 출입구 입지 선정
* 지하철 이용의 혼잡도 문제는 단순히 지하철 내부의 현상을 넘어서, 외부로까지 이어짐 
* 위에 언급한 대각선 신호의 문제와 더불어, <strong>출입구의 적절한 위치 선정은 매우 중요한 사항에 해당</strong>
