# PlayData Data Engineering 31th 부동산팀

## fisrst Mini Prject: 청년 주택 임대 현황 파악 및 정보 제공
### 프로세스
  1. 아이디어 구체화-스토리라인 잡기
  2. 데이터 탐색(if Data is Large: 3번으로 진행.  else 1번부터 다시 시작)
  3. 데이터 추출(크롤링, OpenAPI 등의 방법) 
  4. 데이터 정제 및 적재(Pandas 등의 라이브러리를 활용하여 1번에서 결정한 데이터 속성으로 데이터를 가공 후 데이터베이스로 데이터 적재)
  5. 데이터 시각화 방법 탐색
  6. 데이터 시각화
  7. 1번부터 6번까지의 프로세스 과정에 따라서 포트폴리오 작성(시간이 남을 경우 시간이 부족하면 팀이 아닌 개인으로 작성)

#### [1번 프로세스 진행]  
**04/15 : 부동산 이라는 큰 주제 안에서 목적성을 구체화한 아이디어와 그것에 필요한 데이터 확인**  
> 아이디어 후보 도출

    1. 지하철 혼잡도가 부동산 가격에 미치는 영향
    2. 부동산 가격과 출산율
    3. 1인가구의 증가와 부동산 가격의 상관관계
    4. 범죄율과 부동산 데이터
    5. 부동산 서비스 벤처마킹
  
**04/16 : 조사한 아이디어 후보군 중 아이디어 선정 후 디벨롭**
> - 조사한 아이디어가 특별한 인사이트를 도출을 위한 목적과 데이터 시각화 서비스를 제공하는 것으로 나뉨을 확인 후 프로젝트 기한과 할 수 있는 역량을 점검
> - 부동산 정보을 통해서 데이터 시각화 서비스 제공하는 것으로 아이디어 선정
> - 데이터 시각화 기능 구현을 무엇을 할 지를 결정 후 타겟 서비스를 "청년"으로 설정
> - "청년 주택 임대 현황 파악 및 임대 정보를 제공하는 방향으로 아이디어 선정
> - 스토리라인 설정
>   > - 배경: 젊은 계층의 직주근접이 가능한 도시 내의 전셋값이 천정부지로 솟고 있는 상황
>   > - 지원 방안 : 보통 청년주택이 지역평균 가격의 70~80%수준으로 공급의 실제로 적용되고 있는지를 확인
>   > - 검정: 지역구별로 전월세와 청년주택 가격이 어느정도 차이가 나는지 확인 | 청년주택위치/청년주택 가격 및 주변 전월세 가격데이터
>   > - 정보 제공: 원하는 지역에 임대 주택 가격 현황을 제공
>   > - 분석 및 정보 제공함으로써 데이터 시각화
**04/17 : 데이터 탐색, 추출, 정재 및 적재**
> - **데이터 탐색 및 추출** 
>   > - 소스: SH/LH 매입임대, SH/LH 행복주택, 청년 안심주택, 서울특별시 전월세 실거래가 데이터
>   > - 추출: CSV 파일, Post 방식으로 추출한 json 파일
> - **데이터 정재**
>   > - 구현하고자 하는 기능인 분석을 위한 구체적인 분석(행복주택,매입임대,공공임대,민간임대 분류)
>   > - 시각화 및 분석을 고려한 데이터 속성 명세(테이블 3개 명세)
```sql
    CREATE TABLE allLh (  
      `kindRental` VARCHAR(50) NOT NULL, 
      `adresGu` VARCHAR(50) NOT NULL, 
      `adresWay` VARCHAR(50) NOT NULL, 
      `scaleTot` INT NOT NULL, 
      `kindHouse` VARCHAR(50) NOT NULL,
      `totArea` INT NOT NULL,
      `depositMoney` INT NOT NULL,
      `rentalMoney` INT NOT NULL
      );
```
```sql
    CREATE TABLE ansim (
	  `kindRental` VARCHAR(50) NOT NULL,
	  `adresGu` VARCHAR(50) NOT NULL,
	  `adresWay` VARCHAR(50) NOT NULL,
	  `scaleTot` INT NOT NULL,
	  `kindHouse` VARCHAR(50) NOT NULL,
	  `totArea`  INT NOT NULL,
	  `publicdepositMoney` INT NOT NULL,
	  `publicmoneyRental` INT NOT NULL,
	  `privateMoneyDepositLow` INT NOT NULL,
	  `privateMoneyDepositHigh` INT NOT NULL,
	  `privateMoneyRentalLow` INT NOT NULL,
	  `privateMoneyRentalHigh` INT NOT NULL
    );
```
```sql
    CREATE TABLE allRent (
    `yearReg` int, 
    `adresGu` VARCHAR(50) NOT NULL, 
    `division` VARCHAR(50) NOT NULL,
		`totArea` FLOAT NOT NULL, 
    `depositMoney` INT NOT NULL,
    `rentalMoney` INT NOT NULL,
    `divisionContract` VARCHAR(50) NOT NULL
    );
```
    
2024.04.17 수정사항
- 

