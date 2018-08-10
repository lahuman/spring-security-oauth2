# spring security oauth2

백기선님 방송을 보면서 따라 하기!

## Step 1 Spring with Security == tag : V1.0
[[스프링 가이드] 스프링 시큐리티를 살짝 얹어보자](https://www.youtube.com/watch?v=zANzxwy4y3k)

## Step 2 Update UserDetailService == tag : V2.0
[스프링 시큐리티 이것부터 고쳐 쓰세요](https://www.youtube.com/watch?v=fG21HKnYt6g)

## Step 3 Use SpringSecurity with OAuth2 == tag : v3.0
[스프링 시큐리티 OAuth 2 라이브 코딩](https://www.youtube.com/watch?v=NQM1hghpF0Q)

## TEST

### 토큰 가져오기
~~~
http://localhost:8080/oauth/token

Authorization => base auth : 
username => lahuman-client
password => lahuman-password

Body => x-www-form-urlencoded :
key : value
username : lahuman
password : 1234
grant_type : password
~~~

### 토큰 결과 샘플
~~~
{
    "access_token": "2bbecede-a6d1-46f5-a3f4-bad9831ed46a",
    "token_type": "bearer",
    "refresh_token": "cc02f58d-1123-4fc6-a4c0-bd8b9363ce05",
    "expires_in": 3599,
    "scope": "read write trust"
}
~~~

### refresh_token 요청
~~~
http://localhost:8080/oauth/token

Authorization => base auth : 
username => lahuman-client
password => lahuman-password

Body => x-www-form-urlencoded :
key : value
username : lahuman
password : 1234
grant_type : refresh_token
refresh_token : cc02f58d-1123-4fc6-a4c0-bd8b9363ce05
~~~

### refresh_token 결과
~~~
{
    "access_token": "2bbecede-a6d1-46f5-a3f4-bad9831ed46a",
    "token_type": "bearer",
    "refresh_token": "cc02f58d-1123-4fc6-a4c0-bd8b9363ce05",
    "expires_in": 3599,
    "scope": "read write trust"
}
~~~

### 요청 테스트
~~~
http://localhost:8080/users/user

Headers :
key : value
Authorization : bearer 2bbecede-a6d1-46f5-a3f4-bad9831ed46a
~~~

### 요청 결과
~~~
[
    {
        "id": 1,
        "password": "{bcrypt}$2a$10$9oYwvTlP7cQp4fmrbTC7C.NpTjJIhc5bZzmHqhw/lj0.ff3BuPEqW",
        "email": "lahuman@daum.net",
        "username": "lahuman"
    }
]
~~~