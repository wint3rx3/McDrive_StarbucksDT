# McDrive_StarbucksDT

## 1. 문제 정의

드라이브 스루는 우리 삶 곁의 하나의 양식으로 이미 성공적으로 자리 잡았습니다. 코로나 사회 속에서도 드라이브 스루 방법을 통해 검진을 진행하는 등 다양한 분야로의 시도가 이루어졌습니다. 공격적으로 점포를 늘려가는 회사들을 보며 어떤 차량 접근성 변수와 경제적인 요인들이 매장 위치 및 매출에 영향을 미치는지 알아보고자 하였습니다.



따라서 직접 맥드라이브 점주가 되어서, 최적의 장소를 선정하기 위해 기존의 맥드라이브, 그리고 드라이브 스루를 마찬가지로 공격적으로 확장하고 있는 스타벅스 DT의 데이터를 이용하여 프로젝트를 진행해 보았습니다.

## 2. 데이터 수집
- **매장 정보**
  - [맥도날드 공식 홈페이지](https://www.mcdonalds.co.kr/kor/store/main.do)
  - [스타벅스 공식 홈페이지](https://www.starbucks.co.kr/store/store_map.do)
    
- **상권 정보 (700m 반경)**
  - [소상공인 진흥 공단](https://sg.sbiz.or.kr/godo/index.sg)
    
- **추가 데이터**
  - [산업통상자원부 주유소 데이터](https://www.data.go.kr/data/15129441/standard.do)
  - [문화체육관광부 관광지 데이터](https://www.data.go.kr/data/15021141/standard.do)
  - [국토교통부 공시지가 데이터](https://www.data.go.kr/data/15029071/standard.do)

## 3. 데이터 전처리

- **결측치 확인** : 주소의 변경으로 인해 결측치를 수작업으로 처리함 (ex. 부천시 지역구)
- **사용한 데이터** : 변수 이름과 설명 (상권 정보의 반경 : 700m, 주유소 및 관광지 : 1km)

  | 변수명                      | 설명                                  |
  |---------------------------|-------------------------------------|
  | Upso                      | 반경 내 업소 수                         |
  | FlowPop                   | 유동인구                              |
  | EmpPop                    | 직장인구                              |
  | AbodePop                  | 주거인구                              |
  | EmpAvgCo                  | 직장 평균 매출 (혹은 기타 매출 관련 지표)     |
  | LandPrice                 | 공시지가                              |
  | SalesAmt                  | 월 평균 매출액                          |
  | station_within_radius     | 반경 내 주유소 수                        |
  | closest_station_distance  | 최근접 주유소 거리                       |
  | tourist_within_radius     | 반경 내 관광지 수                        |
  | closest_tourist_distance  | 최근접 관광지 거리                       |

- **분석 반경:**  
  - 상권 정보: 700m  
  - 주유소 및 관광지: 1km

## 4. 탐색적 데이터 분석 (EDA)

- **업종별 차이 분석:**  
  맥도날드와 스타벅스는 각각 패스트푸드와 커피 업종임에도 불구하고, 상권 정보 분포가 유사함을 확인.
  ![image](https://github.com/user-attachments/assets/3ec29f81-4bf2-42e1-85b1-3d5660ab78ea)

  
- **지도 시각화:**  
  SPOTFIRE를 활용하여 수도권 내 맥드라이브와 스타벅스 DT 매장의 위치를 시각화.
  ![image](https://github.com/user-attachments/assets/e0ba5e08-3755-4ee0-9926-9967f6d9d267)


## 5. 모델링 및 분석

1. **매장 군집화**  
   - **알고리즘:** K-means, DBSCAN  
   - **목표:** 매장을 관광지형, 교통인접형, 상권가형, 주택단지형 등으로 분류
     
   ![image](https://github.com/user-attachments/assets/20cacbd4-c039-4999-a8da-02333ac5f032)


2. **매출 예상 모델링**  
   - **모델:** 다중 선형 회귀, 의사 결정 나무, SVM  
   - **분석 대상:** 전체 매장, 업종별(패스트푸드, 카페) 및 군집 기반 성능 비교
     
   ![image](https://github.com/user-attachments/assets/5213c6ad-4cce-419e-b478-a4d7f8cc7499)


## 6. 모델링 결과

  ![image](https://github.com/user-attachments/assets/ba05b875-7475-4666-a478-c331f2f72383)
  ~~기대에 미치지 못하는 성능 (폭망) ~~

## 프로젝트 후 느낀 점

- **실제 데이터 다루기:**  
  이론에서 배운 머신러닝 기법을 실제 데이터 분석에 적용하며 여러 어려움과 한계를 체감.
  
- **웹 스크래핑 경험:**  
  직접 데이터를 수집하며 웹 스크래핑 및 매크로 작성의 중요성을 깨달음.
  
- **API 활용:**  
  카카오 REST API와 Google Maps API를 활용해 좌표 변환 및 시각화를 진행하였으나, 공식 홈페이지에서 제공하는 데이터를 사용할 수 있어 API 활용의 필요성이 줄어듦.
  
- **데이터의 중요성:**  
  드라이브 스루 매장 데이터의 수가 적어, 데이터 증강 시도에도 불구하고 성능 향상에 한계가 있었음.

## 참고자료

- [스타벅스 DT매장과 맥도날드 DT매장의 위치 시각화](https://velog.io/@now2466/스타벅스-DT매장과-맥도날드-DT매장의-위치-시각화)
- [카카오 REST API (주소 -> 좌표 변환)](https://apis.map.kakao.com/web/sample/addr2coord/)
- [Selenium과 주유소 가격 정보](https://velog.io/@insung_na/Selenium과-주유소-가격-정보)
