---
title: 사용자 정보확인
---
<Block>

# 시용자정보확인

[[toc]]

</Block>

<Block>

## 사용자 아이디 사용유무 확인

사용자의 `userID`  존재유무를 확인한다

````vue
curl -X get http://localhost/api/auth/userCount/$userID
````

### 입력

| param  |  형식   |              설명               | 
| :---: | :-----: | :------------------------------------: | :-----: |
|   userID   | String  |               사용자아이디                |

### 출력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   count   | int  |               1: 사용중 0: 미사용                |

<Example>

<CURL>
```bash
curl -X get http://localhost/api/auth/userCount/unicore
```
</CURL>

</Example>

</Block>

<Block>

## 신규 사용자 등록

신규사용자를 등록한다.

````vue
curl -X post http://localhost/api/auth/userInsert
--data '{
"user_id": "unicoretest001",
"user_password": "unicoretest001",
"user_status": 1,
"user_terms_agree": 1,
"user_address": "서울시 기본주소",
"user_detail_address": "AA아파트 101동 1010호",
"mobile_phone": "0101124457",
"user_email": "email@eemil.com",
"user_name": "테스트사용자",
"user_birth_day": "19000101",
"recommend_id": "unicore001"
}'
````

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   user_id   | String  |               사용자아이디                |
|   user_password   | String  |               패스워드                |
|   user_status   | int  |               사용자이용가능상태 1:이용가능 0:서비스이용불가                |
|   user_terms_agree   | int  |              약관동의 1:동의 0: 미동의                |
|   user_address   | String  |               주소               |
|   user_detail_address   | String  |               세부주소                |
|   mobile_phone   | String  |               핸드폰번호                |
|   user_email   | String  |               사용자이메일                |
|   user_name   | String  |               사용자이름                |
|   user_birth_day   | String  |               생년월일 19000101                |
|   recommend_id   | String  |               추천인아이디                |

### 출력

성공: respons status 200
실패: respons status 500
| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X post http://localhost/api/auth/userInsert
  --data '{
    "user_id": "unicoretest001",
    "user_password": "unicoretest001",
    "user_status": 1,
    "user_terms_agree": 1,
    "user_address": "서울시 기본주소",
    "user_detail_address": "AA아파트 101동 1010호",
    "mobile_phone": "0101124457",
    "user_email": "email@eemil.com",
    "user_name": "테스트사용자",
    "user_birth_day": "19000101",
    "recommend_id": "unicore001"
  }'
```
</CURL>

</Example>

</Block>


<Block>

## 추천인 존재확인

추천인이 존재하는지 확인한다.

````vue
curl -X get http://localhost/api/auth/userName/$userId
````

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   $userId   | String  |             추천인아아디                |

### 출력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   user_id   | String  |      아아디  |
|   user_name   | String  |      이름   |

<Example>

<CURL>
```bash
curl -X get http://localhost/api/auth/userName/unicore
```
</CURL>

</Example>

</Block>

<Block>

## 로그인

로그인을 한다.

````vue
curl -X post http://localhost/api/auth/loginInfo
````

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   user_id   | String  |        사용자 아아디           |
|   user_password   | String  |        사용자 아아디           |

### 출력

#### response 해더값

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   authorization | String  |  api 이용가능 인증키값  |

#### response data

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   user_id | String  |      아아디  |
|   user_password | String  |   패스워드-빈값으로 온다  |
|   user_statuss  | tinyint(1)  |    사용자 상태 1-이용가능 0-이용불가   |
|   user_name  | String  |      이름   |
|   mobile_phone  | String  |    핸드폰번호   |
|   user_birth_day  | String  |   생년월일   |
|   bank_name  | String  |    은행이름   |
|   bank_account  | String  |   은행계좌번호   |
|   bank_holder  | String  |    예금주이름  |
|   recommend_user_id  | String  |   추천인 아이디   |

<Example>

<CURL>
```bash
curl -X get http://localhost/api/auth/userName/unicore
```
</CURL>

</Example>

</Block>


<Block>

## 비밀번호 변경

비밀번호를 변경한다.

````vue
curl -X post http://localhost/api/auth/updatePassword
````
### 입력

#### Request 헤더요청값

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   authorization   | String  |        api 이용가능 인증키값      |

#### 파라미터입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: | :-----: |
|   user_id   | String  |        사용자 아아디           |
|   old_password   | String  |        기존패스워드         |
|   new_password   | String  |        변경하는 패스워드         |

### 출력

response 200(ok)

<Example>

<CURL>
```bash
curl -X post http://localhost/api/auth/updatePassword
  --data '{
    "user_id": "unicoretest001",
    "old_password": "unicoretest001",
    "new_password": "unicoretest002",
  }'
```
</CURL>

</Example>

</Block>



