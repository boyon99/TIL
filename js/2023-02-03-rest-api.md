# REST API
REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍쳐이고 REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미한다.

## REST API의 구성
자원, 행위, 표현 3가지로 구성된다. 
- 자원 : URL(엔드포인트)
- 행위 : HTTP 요청 메서드
- 표현 : 페이로드 

<br/>

## REST API 설계 원칙
1. URL은 리소스를 표현하는데 중점을 두어야 한다. 리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용하며 이름에 get 같은 행위에 대한 표현이 들어가서는 안된다.
```
# good
GET /todos/1
```

2. 행위에 대한 정의는 HTTP 요청 메서드를 통해 표현한다. 주로 5가지 요청 메서드를 사용하여 CURD를 구현한다.
- GET : index로 리소스를 취득한다. (페이로드 X)
- POST : create로 리소스를 생성한다.
- PUT : replace로 리소스의 전체를 교체한다.
- PATCH : modify로 리소스의 일부를 수정한다. 
- DELETE : delete로 리소스를 삭제한다. (페이로드 X)

```
# good
DELETE /todos/1
```

<br/>

## JSON 서버를 이용한 REST API 실습
> [JSON 서버를 통해 REST API를 구현하여 XMLHttpRequest방식으로 요청 응답하기 실습](https://github.com/boyon99/REST-API)에서 실습을 진행하였다.