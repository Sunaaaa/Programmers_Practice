# SQL 

## SELECT

### 모든 레코드 조회하기

```mysql
SELECT * from animal_ins
order by 1;
```



### 역순 정렬하기

```mysql
SELECT name, datetime from animal_ins
order by animal_id DESC;
```



### 아픈 동물 찾기

```mysql
SELECT animal_id, name
from animal_ins
where intake_condition = 'sick'
order by animal_id;
```



### 어린 동물 찾기

```mysql
SELECT animal_id, name from animal_ins
where intake_condition != 'aged';
```



### 동물의 아이디와 이름

```mysql
SELECT animal_id, name from animal_ins
order by 1;
```



### 여러 기준으로 정렬하기

```mysql
SELECT animal_id, name, datetime
from animal_ins
order by name, datetime DESC
```



### 상위 n개 레코드

```mysql
# 상위 1개 레코드
SELECT name from animal_ins
order by datetime
LIMIT 1;
```
