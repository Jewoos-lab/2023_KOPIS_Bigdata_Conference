<div>2023 제 3회 코피스빅데이터 컨퍼런스 최종본선(Top10) 진출 작품</div><br>
<h10 fontsize=3><strong></strong>※ 최종본선 진출 팀의 경우, 대회정책상  자료공유는 따로하지 않았습니다.</strong></h10>
<div>
  <h1>🎖️ 2023 제3회 코피스빅데이터 컨퍼런스<br>
    <br>
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

## 5) 회복탄력성 지수를 토대로, 만약 회복되지 않은 극장이 모두 회복되었다고 가정했다면?
<h3><img width="382" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/a635b8e2-dc86-42d6-b92f-be9209d4290c"></h3>

* 회복탄력성 수치를 기준으로 회복하지 못한 중극장 13개가 정상매출로 회복하였을 경우, 전체 매출은 3.7% 상승할 것으로 예측되었음

## 6) 회복탄력성과 연관있는 변수 파악
<h3><img width="888" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/cbc18927-b01c-40de-81fb-e1299ea68e59"></h3>

* 스피어만, 켄달타우 상관계수 방법론을 모두 적용하여, 연관변수를 파악하고자 하였음

* 그 결과, 각 군집별 회복탄력성에 영향을 미치는 요인을 파악한 결과 두 군집에서 문화시설 개수가 회복탄력성에 정반대되는 양상을 띄는것을 확인하였음

## 7) 회복이 잘 되지 않은 극장과, 회복이 잘 된 극장의 통계적 유의변수 도출
<h3><img width="824" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/8392c2a9-9eeb-4453-9f16-be421e5b28e1">
</h3>

* Man whitey U test를 통하여 각 군집내에서 회복된 극장과 회복 되지 않은 극장의 유의 변수를 도출함

* 그 결과, 군집0에선 금액이 너무 낮지 않은 공연이 구성되었을 때, 좋은 회복력을 기대할 수 있었고,

* 군집1에선 고령층 타겟의 공연이나 행사 기획을 통해 회복을 하지 못한 극장의 회복을 기대할 수 있었음
<br>
<br>

# 📈 결과
## 1) 활용 가능성 및 방향
<h3><img width="851" alt="image" src="https://github.com/Jewoos-lab/2023_KOPIS_Bigdata_Conference/assets/86662870/1f81f74d-2298-4cf2-82ab-17556dd31779"></h3>

* 회복 탄력성 지수 활용 - 공연 문화 시장의 회복 정도를 나타내는 인터페이스 구축

<br>

* 상임드라마투르그 전문가의 보조지표 역할 가능
* 회복력 연관 변수를 활용한 운영 전략 수립
* 시기별 예술 활성화 계획 수립

## 2) 기대효과 및 한계점
<h3>기대효과</h3>

* 회복력 점검
* 정책 수립 기반 마련
* 지역 공연 예술 활성화

<br>
<h3>한계점</h3>

* 비수도권의 공공데이터가 대부분 시군구 단위였기에, 더 세분화된 행정동으로는 데이터를 구할수 없어 공간점 범위에서 한계점이 있었음
* 충격지점 이전에 월별 매출이 1개인 공연시설의 경우, 해당 값으로 예상매출을 지정함

