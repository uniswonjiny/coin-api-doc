---
title: 채굴기 공통 / 기타 정보조회
---
<Block>

# 채굴기 - 유니포인트

[[toc]]

</Block>

<Block>

## 현재 비트코인시세확인

 - 채굴기(th) 판매 업체 목록을 확인한다.

```vue
curl -X get http://localhost/api/com/bitCoinCurrency/${flag}
```
+ 입력

| param  |  형식   |              설명               | 부가설명                           |
| :---: | :-----: | :------------------------------------: |:-------------------------------|
|   flag   | Boolean  |          입력여부           | true: 입력 <br/> flase: 이입력정보만확인 |

 + 출력
   + 성공: respons status 200  
   + 실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X get http://localhost/api/com/bitCoinInfoInsert/false
```
</CURL>

</Example>

</Block>

<Block>

## 현재 비트코인시세정보 입력

- 채굴기(th) 판매 업체 목록을 확인한다.

```vue
curl -X get http://localhost/api/com/bitCoinInfoInsert
```
+ 출력
   + 성공: respons status 200
   + 실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X get http://localhost/api/com/bitCoinInfoInsert
```
</CURL>

</Example>

</Block>

<Block>

## 유니코아 설정 수수료목록

- 유니코아에서 설정한 각종 수수료 정보 물론 대외로 알려도 되는 항목만

```vue
curl -X get http://localhost/api/com/settingFeeList
```
+ 출력
   + 성공: respons status 200

| param  |  형식   |             설명              |
| :---: | :-----: |:---------------------------:|
|   main_type   | String  |          내부주요코드타입           |
|   fee_string   | String  | 주요수수료타입 수수료유형(main_type)한글로 |
|   detail_type   | String  |           내부상세코드            |
|   value   | String  |             실제값             |
|   created_at   | String  |           적용된 날짜            |
|   admin_user_no   | String  |          적용한관리자번호           |
|   memo   | String  |        상세코드나 자세한 내용         |

   + 실패: respons status 500

| param  |  형식   |              설명               |
| :---: | :-----: | :------------------------------------: |
|   message   | String  |               실패한사유|

<Example>

<CURL>
```bash
curl -X get http://localhost/api/com/settingFeeList
```
</CURL>

</Example>

</Block>
