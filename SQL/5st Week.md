# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

📌 DATETIME 함수

- CURRENT_DATETIME : 현재 DATETIME 출력	
~~~
주로 날짜(YYYY-MM-DD)와 시간(HH:MI:SS) 정보가 합쳐진 형태의 데이터를 다루는 데 사용되며, DATETIME은 SQL에서 날짜와 시간을 동시에 저장하는 데이터 타입 이름이기도 합니다.
~~~
---
**CURRENT_DATE() 함수와 시간대(Time Zone) 때문에 발생하는 혼란**

**'2025-11-04 05:00:00'**에 CURRENT_DATE()를 실행하면, 함수는 로컬 시계를 보고 **'2025-11-04'**를 반환합니다.

하지만 이 시점의 UTC 시간은 9시간 느리기 때문에, 아직 '2025-11-03'입니다. (05:00:00 - 9시간 = 전날 20:00:00)

< 정확한 처리를 위한 팁 >

SQL에서 날짜와 시간을 비교할 때는 CURRENT_DATE() 대신 CURRENT_TIMESTAMP() 또는 NOW() 함수를 사용하는 것이 더 안전합니다. 

이 함수들은 시간대 정보가 포함된 정확한 시점을 반환하기 때문에, AT TIME ZONE 함수 등을 사용하여 UTC 기준으로 통일된 날짜를 추출할 수 있습니다.

---

- EXTRACT : 특정 부분만 추출하고 싶은 경우
-> 사용 : 일자별 주문, 월별 주문

	- 요일을 추출 : DAYOFWEEK
		EXTRACT(DAYOFWEEK FROM datetime_col)
		1 : 일요일 / 2 : 월요일 / 7 : 토요일

- DATETIME_TRUNC : DATE & HOUR만 남기고 싶은 경우 => 시간 자르기
	주로 시간(HOUR)을 자를 때 사용!

- PARSE_DATETIME : 문자열 데이터 -> DATETIME 타입 데이터
*PARSING = 문자열을 분석해서 알맞은 것으로 배치한다* 
	- %를 사용 EX. %Y = 년도

- FORMAT_DATETIME : DATETIME 타입 데이터 -> 문자열 데이터

- LAST_DAY : 마지막 날을 알고 싶은 경우 
	자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우

	LAST_DAY에서 WEEK은 기본값 : SUNDAY -> 토요일이 반환

- DATETIME_DIFF : 두 DATETIME의 차이를 알고 싶은 경우

## < 정리 >

날짜 및 시간 데이터 타입

- DATE 
- DATETIME : DATE + TIME. 타임존 정보 X
- TIMESTAMP : 특정 시점에 도장 찍은 값. 타임존 정보 O
- UTC : 국제적인 표준 시간. 한국은 UTC+9
- Millisecond : 1/1000초
- Microsecond : 1/1000ms

시간 데이터 타입 변환하기

- TIMESTAMP_MILLIS : MILLIS -> TIMESTAMP
- TIMESTAMP_MICROS : MICROS -> TIMESTAMP
- 문자열 -> DATETIME : PARSE_DATETIME
- DATETIME -> 문자열 : FORMAT_DATETIME

- 현재 DATETIME : CURRENT_DATETIME
- DATETIME의 특정 부분 추출 : EXTRACT
- DATETIME 특정 부분 자르기 : DATETIME_TRUNC
- DATETIME 차이 구하기 : DATETIME_DIFF


# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### 조건문이란?
- 만약 특정 조건이 충족되면, 어떤 행동을 해라

### 사용하는 방법
1) CASE WHEN
2) IF

### 사용되는 이유
- 특정 카테고리를 하나로 합치는 전처리가 필요

**1) CASE WHEN**
- 여러 조건이 있을 경우 유용
- 순서 중요
	조건1, 조건2에 둘 다 해당하면 앞선 순서를 따름(100>50)
	특히 문자열 함수에서 이슈가 자주 발생

**2) IF**
- 단일 조건일 경우 유용

 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

catch_date : DATE 타입

catch_datetime : UTC. TIMESTAMP 타입 0

=> 컬럼의 이름은 datetime인데 TIMESTAMP 타입으로 저장되어 있다!

원래 datetime : UTC 표현 X -> T 표현 O

(+) catch_date와 catch_datetime을 비교해 본 결과 : UTC는 +9시간을 해야하는데 날짜가 다른 문제 발생
-> catch_date가 KR 기준? / UTC 기준? 

=> 확인 필요!

**4-5 연습문제 1번**

Q. 트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산해주세요. 

SELECT
	
    COUNT(id) AS cnt

FROM 

    basic.trainer_pokemon

WHERE

	EXTRACT(YEAR FROM DATETIME(catch_datetime, "Asia/Seoul")) = 2023 
	AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul")) = 1

- **틀린 부분** : catch_datetime은 TIMESTAMP로 저장되어 있으므로, DATETIME으로 변경해야 한다. 

- **새롭게 알게 된 부분** : 컬럼을 그대로 믿으면 안된다는 점을 알게 되었습니다.

**4-5 연습문제 2번**

 Q. 배틀이 일어난 시간(battle_datetime)을 기준으로, 오전 6시에서 오후 6시 사이에 일어난 배틀의 수를 계산해주세요. 

winner_id : null값 존재
* null : 무승부

    battle_date : battle_datetime 기반으로 만들어진 date
    battle_datetime : T로 표시 O (datetime TRUE)

-> battle_datetime이랑 DATETIME(battle_timestamp, "Asia/Seoul") 같은지 확인 필요!

### 방법

SELECT
	
	COUNTIF(battle_datetime = DATETIME(battle_timestamp, "Asia/Seoul")) AS battle_datetime_same_battle_timestamp_kr,
	
	COUNTIF(battle_datetime != DATETIME(battle_timestamp, "Asia/Seoul")) AS battle_datetime_not_same_battle_timestamp_kr

FROM

	basic.battle

### 문제 풀이
SELECT
	
    COUNT(id) AS battle_cnt

FROM 

    basic.battle

WHERE

	EXTRACT(HOUR FROM battle_datetime) >= 6
	AND EXTRACT(HOUR FROM battle_datetime) <= 18

- **새롭게 알게 된 부분** : EXTRACT 부분이 겹치기 때문에 BETWEEN 사용 가능!
-> BETWEEN a and b : a와 b사이에 있는 것을 반환

**4-7 연습문제 1번**

Q. 포켓몬의 'Speed'가 70이상이면 '빠름', 그렇지 않으면 '느림'으로 표시하는 새로운 컬럼 'Speed_Category'를 만들어주세요

SELECT
	
	IF(speed >= 70, '빠름', '느림') As Speed_Category
FROM 
	
	basic.pokemon

**4-7 연습문제 2번**

Q. 포켓몬의 'type1'에 따라 'Water', 'Fire', 'Electric' 타입은 각각 '물', '불', '전기'로, 그외 타입은 '기타'로 분류하는 새로운 컬럼 'type_Korean'을 만들어 주세요

SELECT
	
	CASE
		WHEN type1 = 'Water' THEN '물'
		WHEN type1 = 'Fire' THEN '불'
		WHEN type1 = 'Electric' THEN '전기'
		ELSE '기타'
	END AS type1_Korean

FROM 
	
	basic.pokemon

<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
틀린 쿼리 : 3번 쿼리 
login_date = '2021'는 문자열 '2021'이다. 이를 날짜 타입과 직접 비교하면 오류가 발생한다. 

원인 : 데이터베이스마다 자동 형 변환이 다르게 이루어지기 때문이다.

틀린 쿼리 : 4번 쿼리 
BETWEEN '2021-01-01' AND '2021-12-31'은 login_date가 TIMESTAMP형이라면 12월 31일 자정 이후는 포함되지 않을 수 있다. 
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
여기에 답을 작성해주세요!
~~~

![alt text](Images_5/수강.png)

<br>

### 🎉 수고하셨습니다.