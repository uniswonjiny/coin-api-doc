---
title: 채굴기 유니포인트 정보
---
<Block>

# 채굴기 - 유니포인트

[[toc]]

</Block>

<Block>

## 구매처확인

 - 채굴기(th) 판매 업체 목록을 확인한다.

```vue
curl -X post http://localhost/api/account/buyCompanyList
--data '{
"start_date": "2022-03-01",
"end_date": "2022-12-31",
"size": 1000,
"start_no": 0,
"status": 1,
}
```
 - 입력

| param  |   형식    |   설명 | 
| :--- |:-------:|----------------------------------------------:|
|   start_date   | String  |  등록일 검색시작일 <br/> null 가능 |
|   end_date   | String  |                       등록일 검색종료일 <br/> null 가능 |
|   size   |   int   |                         검색할 갯수  <br/> null 가능 |
|   start_no   |   int   |                  검색시작 번호 시작=(0) <br/> null 가능 |
|   no   |   int   | 1개를 조회할경우(업체내부 저장번호) 목록에서 선택한경우 <br/> null 가능 |

 + 출력
   + 성공: respons status 200  
   + 실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/buyCompanyList
  --data '{
    "start_date": "2022-03-01",
    "end_date": "2022-12-31",
    "size": 1000,
    "start_no": 0,
    "status": 1,
    "no": null
  }'
```
</CURL>

</Example>

</Block>

<Block>

## 구매처등록

채굴기(th) 판매 업체를 등록한다.

```vue
curl -X post http://localhost/api/account/buyCompany
--data {
"company_name": "kingKong",
"coin_type": "bit_coin",
"position": "AS01",
"fee_type": 'bit_coin',
"fee": 0.00000001,
"admin_user_no": 1,
"status": 1,
"charge_name": "킹콩관리직원",
"charge_contact": "테스트사용자"
}
```

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   company_name   | String  |           회사이름           |
|   coin_type   | String  |           코인유형(*bit_coin)           |
|   position   | String  |       채굴기위치          |
|   fee_type   | String  |               관리비타입                |
|   fee   | decimal(20,8)  |          관리비           |
|   admin_user_no   | Number  |          관리자이용자번호           |
|   status   | Number  |        사용가능상태(0:미사용 1:사용)            |
|   memo   | String  |            메모              |
|   charge_name   | String  |             담당자이름                |
|   charge_contact   | String  |         담당자연락처           |

### 출력

성공: respons status 200
실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/buyCompany
  --data '{
    "company_name": "kingKong",
    "coin_type": "bit_coin",
    "position": "AS01",
    "fee_type": "bit_coin",
    "fee": 1,
    "admin_user_no": 1,
    "status": 1,
    "memo": "",
    "charge_name": "킹콩관리직원",
    "charge_contact": "테스트사용자"
  }'
```
</CURL>

</Example>

</Block>


<Block>

## 채굴기 구매 - 포인트(재고) 추가

실제 업체로부터 채굴기를 구매기록및 판매가능 포인트를 추가한다.

```vue
curl -X post http://localhost/api/account/pointThBuy
--data {
"buy_date": "2022-03-20",
"purchase_no": 1,
"amount": "11000000",
"th": 100,
"uni_point": 10,
"created_user_no": 1
}
```

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   buy_date   | String  |           구매일자 <br/> Null 현재날짜           |
|   purchase_no   | Number  |           1(구매처+장비위치 선택할경우 내부값)      |
|   amount   | Number  |               구매금액                |
|   th   | Number  |          채굴기           |
|   uni_point   | Number  |         th 환산 포인트(화면에서 계산될내용)          |
|   created_user_no   | Number  |     등록한 사용자 번호      |

### 출력

>성공: respons status 200
>실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/pointThBuy
  --data '{
    "buy_date": "2022-03-20",
    "purchase_no": 1,
    "amount": "11000000",
    "th": 100,
    "uni_point": 10,
    "created_user_no": 1
  }'
```
</CURL>

</Example>

</Block>

<Block>

## 채굴기 구매확정 - 포인트(재고) 추가

>채굴기 구매 송금일자 완료처리 , 채굴시작

```vue
curl -X post http://localhost/api/account/pointThBuyUpdate
--data {
"type": "T",
"target_date": "2022-03-22",
"no": 1,
"admin_user_no": 1
}
```

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   type   | String  |           요청타입 <br/>P = 송금완료<br/>T = 채굴시작        |
|   target_date   | Number  |           요청하는 날짜(2022-01-01)     |
|   no   | Number  |        해당장비번호        |
|   admin_user_no   | Number  |     등록한 사용자 번호      |

### 출력

>성공: respons status 200
>실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/pointThBuyUpdate
  --data '{
        "type": "T",
        "target_date": "2022-03-22",
        "no": 1,
        "admin_user_no": 1
  }'
```
</CURL>

</Example>

</Block>

<Block>

## 채굴기 목록확인

채굴기 구매상태등 목록확인

```vue
curl -X post http://localhost/api/account/pointThList
    --data {
    "start_date": "2022-03-22",
    "end_date": "2022-03-22",
    "no": 1,
    "status": 1,
    "purchase_no": 1
}
```

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   start_date   | String  |       검색시작일<br/>Null 가능        |
|   end_date   | String  |      검색종료일<br/>Null 가능     |
|   no   | Number  |        해당장비번호 <br/>Null 가능       |
|   status   | String  |     장비상태  <br/>Null 가능    |
|   purchase_no   | Number  |     구매처+장비위치번호<br/>Null 가능      |

### 출력

성공: respons status 200
실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   buy_date   | String  |     구매일자     |
|   payment_date   | String  |    송금일자|
|   status   | String  |         동작가능상태<br/> F 미작동<br/> R 대기중<br/> P 입금만된상태<br/> T 작동 - 채굴시작|
|   purchase_no   | String  |       구매처장비위치번호|
|   th   | Number  |               채굴기수량|
|   uni_point   | Number  |               유니포인트수량|
|   created_user_no   | Number  |               최초생성한 관리자번호|
|   updated_user_no   | Number  |               수정한 관리자번호|
|   start_date   | String  |               채굴시작일|
|   end_date   | String  |               채굴종료일|
|   created_at   | String  |               생성일시|
|   updated_at   | String  |               수정일시|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/pointThList
  --data '{
    "start_date": "1900-01-01",
    "end_date": "2999-12-31",
    "no": "",
    "status": "",
    "purchase_no": ""
  }'
```
</CURL>

</Example>

</Block>

<Block>

## 사용자 유니포인트 내역확인

- 사용자들의 포인트 구매 내역을 확인한다
```vue
curl -X get http://localhost/api/account/uniPointList/:userId
-H 'authorization:  :authorization'
```

### 입력

| param  |  형식   |     설명      | 비고 |
|:------:| :-----: |:-----------:|--|
| userId | String  |   사용자아아디    | 주소뒤에 입력 |
| authorization | String  | 인증키 | 로그인시 받은 인증키를 헤더에 입력 |


### 출력

>성공: respons status 200
 - userSumInfo : 현재 사용자의 요약정보

| param  |      형식       |   설명   |
| :---: |:-------------:|:------:|
|   uni_point   |      int      | 유니포인트  |
|   btc_point   | decimal(10,8) |  비트코인  |
|   money   |      int      | 사용한 현찰 |
|   type   |    String     |  구매유형  |

 - userPointList : 사용자의 포인트 구매관련내역정보

| param  |      형식       |   설명   |
| :---: |:-------------:|:------:|
|   no   |      int      | 순번  |
|   user_no   | int |  사용자번호  |
|   sales_type   |      String      | 판매유형 |
|   type   |    String     |  구매유형  |
|   money   |    int     |  구매금액  |
|   tax   |    int     |  세금  |
|   document_type   |    String     |  소득증빙약식코드  |
|   uni_point   |    int     |  유니포인트  |
|   document_number   |    String     |  소득증명번호등  |
|   start_date   |    Date     |  채굴시작일  |

>실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X get http://localhost/api/account/uniPointList/:userId
-H 'authorization:  12345'
```
</CURL>

</Example>

</Block>

<Block>

## 사용자 유니포인트 구매

- 사용자의 유니포인트 구매
```vue
curl -X post http://localhost/api/account/buyUniPoint
--data {
    "user_id": "uniocre001",
    "money": 1000000,
    "tax": 100000 ,
    "uni_point": 1,
    "document_type": "E",
    "document_number": "1254-457878"
}
```

### 입력

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   user_id   | String  |      사용자아아디     |
|   money   | Number  |     구매금액        |
|   tax   | Number  |        부가세        |
|   uni_point   | Number  |     유니포인트      |
|   document_type   | String  |     증빙서류종류 <br/> I-소득공제 <br/> E-지출증빙      |
|   document_number   | String  |     증빙서류번호      |


### 출력

>성공: respons status 200

>실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X POST http://localhost/api/account/buyUniPoint
  --data '{
    "user_id": "user001",
    "money": 1000000,
    "tax": 100000 ,
    "uni_point": 1,
    "document_type": "E",
    "document_number": "1254-457878"
  }'
```
</CURL>

</Example>

</Block>

<Block>

## 사용자 유니포인트 확정

- 사용자의 유니포인트 구매 / 환불 확정하기
```vue
curl -X post http://localhost/api/account/uniPointConfirm
-H 'authorization:  :authorization'
--data {
    "no": "1",
    "confirmType": "Y"
}
```

### 입력

| param |   형식   |                설명                 | 비고 |
|:-----:|:------:|:---------------------------------:|--|
|  no   |  int   |             유니포인트목록번호             | 구매번호는 사용자구분없이 <br/>유니크한 고유번호 |
|   confirmType    | String | 구매/환불 구분요청자 |  Y= 구매확정 <br/> P = 환불확정 |
|   authorization    | String |                인증키                | 로그인시 받은 인증키를 헤더에 입력해야함 |


### 출력

>성공: respons status 200

>실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>

```bash
curl -X POST http://localhost/api/account/uniPointConfirm
-H 'authorization:  :authorization'
  --data '{
    "no": "1",
    "confirmType": "Y"
  }'
```

</CURL>

</Example>

</Block>
