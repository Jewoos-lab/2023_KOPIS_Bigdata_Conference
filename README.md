<div>2023 제 3회 코피스빅데이터 컨퍼런스 최종본선(Top10) 진출 작품</div><br>
<div>
  <h1>🎖️ 2023 제3회 코피스빅데이터 컨퍼런스<br>
    <br>
   📈 회복탄력성 지수 개발을 통한 공연시설 현황 파악</h1>
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

# 💡 분석 개요
* 코로나로 제한이 풀리면서 상권 매출의 회복탄력성 연구는 늘고있지만, 문화예술에서는 부족한 실정임
* 수도권 공연시장의 회복세는 팬데믹 이후 꾸준히 상승<br>
* 비수도권 내에서도 지역별 공연시장 회복 정도의 확연한 차이 존재<br>
* 대극장과 소극장의 경우 팬데믹 전후 공연매출에 큰 차이가 없었지만 중극장의 경우 매출이 하락세임<br>
<br>
<br>

# 🔎 가설수립 (가설검증은 거의 맨 아래에 작성됨)
1) 경제성
   * 지역의 경제성은 회복력에 영향을 미칠 것이다.
2) 접근성
   * 지역의 접근성은 회복력에 영향을 미칠 것이다.
3) 공연검색량
   * 지역의 공연검색량은 회복에 영향을 미칠 것이다.
<br>

# 데이터 전처리
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
</h3>

* Scree Plot을 활용하여 고유값이 1보다 크면서 해석 가능한 수준인 3개의 요인 추출

* 요인 적재값 도출을 통한 각 요인별 특징 도출

* 이때, 요인분석 결과에 대한 신뢰성 검증을 위해 Tucker Lewis's reliability를 사용하였고, 해당값이 0.6 이상으로 도출되어 적합한 것으로 확인

## 4) 요인회전 및 요인점수 계산
* PCA를 통하여 변수의 축을 최소화하였고, 이를 통해 요인적재값을 도출하였기 때문에 요인별 상관성은 없는것으로 나타남
* 따라서 직교회전의 Varimax를 적용하였음
* 그 후, 요인점수 도출에 요인 적재값을 가중치로 사용하여 요인점수를 계산함<br>
요인점수 계산식
<h3><img width="530" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/c409db83-5fc1-4085-8642-2a9265ecf9bf"></h3>


## 5) 공연시설 군집분석
<h3><img width="994" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/f90d89f2-590c-4af9-92a9-2fdd2c05a810"></h3>

* 클러스터링 대상 변수를 위에서 도출한 공연시설별 요인점수로 지정함

* 군집분석의 결과향상을 위하여 요인점수의 비대칭성 보완을 위하여 로그변환후 정규분포로 수정함

* Kmeans++ 군집분석 기법을 이용하여 극장을 유형화 하였으며, 군집분석의 결과확인을 위하여 실루엣계수와 군집의 너비를 모두 고려하여 최적의 K선정함

## 6) 군집분석 결과
<h3><img width="924" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/ddf047a1-8054-45fe-9cac-89e980be01d8"></h3>

* 규모 및 경제성과 편의성 및 인프라를 나타내는 요인은 두 군집에서 동일한 수준

* 접근성 및 인구특성을 나타내는 요인에서 두 군집별 차이가 확연히 나타나 위와 같이 군집해석을 진행

<br>
<br>

# 📈 회복탄력성 분석
## 1) 극장별 예상매출액 도출
<h3><img width="911" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/436296e4-0414-43d3-8a62-43f25ef3ad02">
</h3>

* 회복탄력성을 구하기 위해선 극장별 예상 매출액을 도출하는 과정은 필수적임

* 예상매출액 도출은 주관적인 개입이 들어가선 안됨
  
* 따라서 공정거래위원회의 실제 예상매출액 산정법을 이용하여 공연시설 예상매출액 도출을 진행하였음

<br>

## 2) 군집 유형별 인사이트 도출
<h3><img width="396" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/f03c9a16-1ba7-4218-8a35-897a21672b05"></h3>

* 군집 0의 예상 매출액 평균이 군집1보다 큰 양상을 보임

* <strong>이는 회복탄력성 지수의 해석을 군집마다 별도로 진행해야 한다는 인사이트임</strong>


## 3) 충격회복력, 충격반응력, 회복탄력성 도출
<h3><img width="872" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/01cad806-30ef-46f6-8753-040c5cbcde97">
</h3>

* 회복탄력성 연구를 참고하여 충격회복력, 충격반응력, 회복탄력성을 도출하였음

* <strong>ratio(비율)의 경우, 위에서 도출한 공연시설 유형별 특징이 매우 다르다는 점과, 예상매출액 차이가 크다는 인사이트를 참고하여 군집0과 군집1에서 각각 산출하여 회복탄력성 공식에 대입하였음</strong>


## 4) 열지도 시각화
<h3><img width="451" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/9f6e181a-cdc8-4d2c-98cd-b8db804238b2"></h3>

* 각 공연시설별로 회복탄력성을 도출하여, 해당 지수를 토대로 핫스팟(회복이 빠른지역)과 콜드스팟(회복이 더딘지역)을 나누어 시각화하였음

## 5) 회복탄력성 지수를 토대로, 만약 회복되지 않은 극장이 모두 회복되었다고 가정한다면?
<h3><img width="382" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/a635b8e2-dc86-42d6-b92f-be9209d4290c"></h3>

* 회복탄력성 수치를 기준으로 회복하지 못한 중극장 13개가 정상매출로 회복하였을 경우, 전체 매출은 3.7% 상승할 것으로 예측되었음

## 6) 회복탄력성과 연관있는 변수 파악
<h3><img width="888" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/cbc18927-b01c-40de-81fb-e1299ea68e59"></h3>

* 스피어만, 켄달타우 상관계수 방법론을 모두 적용하여, 연관변수를 파악하고자 하였음

* 그 결과, 각 군집별 회복탄력성에 영향을 미치는 요인을 파악한 결과 두 군집에서 문화시설 개수가 회복탄력성에 정반대되는 양상을 띄는것을 확인하였음

## 7) 가설검증
<h3><img width="760" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/cc86543d-98d4-412a-ba0d-84c89ac18f79">
</h3>

* Man whitey U test를 통한 가설검증(분석 초기에 수립한 가설을 검증하는 부분임)
1) 경제성
   * 귀무가설(H0): 회복 극장의 지역은 비회복 극장의 지역과 지역 경제성 차이가 없을 것이다.
   * 대립가설(H1): 회복 극장의 지역은 비회복 극장의 지역과 지역 경제성 차이가 있을 것이다.
   * p_value(0.049) < a(0.05)으로 인한 가설 채택 -> 회복극장과 비회복극장은 경제성에서 유의한 차이를 보인다.
2) 평균연령
   * 귀무가설(H0): 회복 극장의 지역은 비회복 극장의 지역과 평균연령의 차이가 없을 것이다.
   * 대립가설(H1): 회복 극장의 지역은 비회복 극장의 지역과 평균연령의 차이가 있을 것이다.
   * p_value(0.049) < a(0.05)으로 인한 가설 채택 -> 회복극장과 비회복극장은 평균연령에서 유의한 차이를 보인다.
3) 공연검색량
   * 귀무가설(H0): 회복 극장의 지역은 비회복 극장의 지역과 공연검색량의 차이가 없을 것이다. 
   * 대립가설(H1): 회복 극장의 지역은 비회복 극장의 지역과 공검색량의 차이가 있을 것이다.
   * p_value(0.5) > a(0.05)으로 인한 가설 기각 -> 공연검색량은 회복극장과 비회복극장은 공연검색량에서 차이가 없다.

<br>
<br>

# 📈 결과의의
가설 1 -> 지역 경제성과 공연시설 회복탄력성
의의: 이 결과는 지역의 경제적 상황이 공연시설의 회복탄력성에 영향을 미칠 수 있다는 가정을 뒷받침합니다. 경제적으로 안정된 지역에서는 문화적 활동에 대한 수요가 더 빠르게 회복될 수 있으며, 이는 문화 및 예술 산업에 대한 정책적인 중요성을 강조합니다.

가설 2 -> 지역별 평균 연령과 공연시설 회복탄력성
의의: 이 결과는 지역의 평균 연령이 공연시설의 회복탄력성에 영향을 미칠 수 있다는 가정을 뒷받침합니다. 다양한 연령대의 문화적 선호도를 고려하여 공연 프로그램을 제공하는 것이 중요함을 시사합니다.

가설 3 -> 지역별 공연 검색량과 공연시설 회복탄력성
의의: 이 결과는 공연 검색량이 공연시설의 회복탄력성과 직접적인 연관성이 없다는 것을 나타냅니다. 이는 공연 홍보나 마케팅 전략을 다시 평가하고 다양한 방법으로 지역 사회에 접근할 필요가 있음을 시사합니다.


## 2) 기대효과 및 한계점
<h3>기대효과</h3>

* 회복력 점검
* 정책 수립 기반 마련
* 지역 공연 예술 활성화

<br>
<h3>한계점</h3>

* 비수도권의 공공데이터가 대부분 시군구 단위였기에, 더 세분화된 행정동으로는 데이터를 구할수 없어 공간점 범위에서 한계점이 있었음
* 충격지점 이전에 월별 매출이 1개인 공연시설의 경우, 해당 값으로 예상매출을 지정함

