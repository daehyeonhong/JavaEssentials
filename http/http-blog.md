# HTTP Web Basic Knowledge

## HTTP Method 활용

### `Client`에서 `Server`로 데이터 전송

- static data 조회
- query parameter 조회

```http request
GET /static/star.jpg HTTP/1.1
Host: localhost:8080
```

```http response
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 1234

${load image data}
```

- dynamic data 조회

```http request
GET /dynamic/example?kim=0 HTTP/1.1
Host: localhost:8080
```

```http response
HTTP/1.1 200 OK
```

- `query parameter`를 통해 `dynamic data`를 조회하고, `response`로 `200 OK`를 반환한다.

- `HTML Form`을 통해 데이터 전송

#### 1. `POST` 방식으로 전송

```html

<form action="/dynamic/example" method="post">
    <input type="text" name="kim" value="0">
    <button type="submit">전송</button>
</form>
```

```http request
POST /dynamic/example HTTP/1.1
Host: localhost:8080
Content-Type: application/x-www-form-urlencoded

kim=0
```

```http response
HTTP/1.1 200 OK
```

- `HTML Form`을 통해 `POST` 방식으로 데이터를 전송하면 `Content-Type`이 `application/x-www-form-urlencoded`로 설정되고, `query parameter`와
  동일하게 `key=value` 형태로 전송된다.

#### 2. `GET` 방식으로 전송

```html

<form action="/dynamic/example" method="get">
    <input type="text" name="kim" value="0">
    <button type="submit">전송</button>
</form>
```

```http request
GET /dynamic/example?kim=0 HTTP/1.1
Host: localhost:8080
```

- `HTML Form`을 통해 `GET` 방식으로 데이터를 전송하면 `query parameter`와 동일하게 전송된다.

- multipart/form-data

```html

<form action="/save" method="post" enctype="multipart/form-data">
    <input type="text" name="username">
    <input type="file" name="file1">
    <input type="file" name="file2">
    <button type="submit">전송</button>
</form>
```

```http request
POST /save HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Length: 1234

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

kim
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file1"; filename="hello.txt"

hello
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file2"; filename="test.txt"

test
------WebKitFormBoundary7MA4YWxkTrZu0gW--
``` 

- `HTML Form`을 통해 `multipart/form-data`로 데이터를 전송하면 `Content-Type`이 `multipart/form-data`로 설정되고, `boundary`를 통해
  `key=value` 형태로 전송된다.
- `boundary`는 `Content-Type`에 설정된 `boundary`와 `key=value` 형태의 데이터를 구분하는 역할을 한다.

- `HTTP API` 형태로 데이터 전송

```http request
POST /save HTTP/1.1
Host: localhost:8080
Content-Type: application/json

{
    "username": "kim",
    "age": 20
}
```

```http response
HTTP/1.1 200 OK
```

- `HTTP API` 형태로 데이터를 전송하면 `Content-Type`이 `application/json`으로 설정되고, `JSON` 형태로 전송된다.
- `application/json`의 기본 `charset`은 `UTF-8`이다.

### HTTP API 설계 예시

#### 1. 회원 관리 시스템(Collection)

| API 동작   | 경로            | HTTP 메서드         |
|----------|---------------|------------------|
| 회원 목록 조회 | /members      | GET              |
| 회원 등록    | /members      | POST             |
| 회원 조회    | /members/{id} | GET              |
| 회원 수정    | /members/{id} | PATCH, PUT, POST |
| 회원 삭제    | /members/{id} | DELETE           |

- `Collection`은 서버가 관리하는 리소스 저장소를 의미한다.
- 클라이언트는 등록 요청을 할 때, 등록될 리소스의 `URI`를 모른다.
- `Collection`은 복수형으로 사용하는 것이 좋다. ex) /members, /orders
- `Collection`에서 등록은 `POST`를 사용한다.

#### 2. 파일 관리 시스템(Store)

| API 동작   | 경로                | HTTP 메서드 |
|----------|-------------------|----------|
| 파일 목록 조회 | /files            | GET      |
| 파일 조회    | /files/{filename} | GET      |
| 파일 등록    | /files/{filename} | PUT      |
| 파일 삭제    | /files/{filename} | DELETE   |
| 파일 대량 등록 | /files            | POST     |

- `Store`는 클라이언트가 관리하는 리소스 저장소를 의미한다.
- 클라이언트는 등록 요청을 할 때, 등록될 리소스의 `URI`를 알고 있다.
- `Store`의 등록은 `PUT`을 사용한다.

#### 3. HTML Form 사용

| API 동작   | 경로                                | HTTP 메서드 |
|----------|-----------------------------------|----------|
| 회원 목록 조회 | /members                          | GET      |
| 회원 등록 폼  | /members/new                      | GET      |
| 회원 등록    | /members/new, /members            | POST     |
| 회원 조회    | /members/{id}                     | GET      |
| 회원 수정 폼  | /members/{id}/edit                | GET      |
| 회원 수정    | /members/{id}/edit, /members/{id} | POST     |
| 회원 삭제    | /members/{id}/delete              | POST     |

`HTML Form`을 사용하면 `GET`, `POST`만 사용할 수 있으며, `PUT`, `PATCH`, `DELETE`를 사용할 수 없다.

때문에 두 가지 메서드로 다양한 동작을 수행하기 위해 `URI`에 동작을 명시한다(동사 사용).

`HTTP 메서드`로 동작을 구분하기 어려운 경우, `URI`에 동작을 명시하여 사용하기도 한다.

### HTTP Status Code

| 분류  | 종류            | 설명                                     |
|-----|---------------|----------------------------------------|
| 1xx | Informational | 요청이 수신되어 처리중이다.                        |
| 2xx | Success       | 요청 정상 처리되었다.                           |
| 3xx | Redirection   | 요청을 완료하려면 추가 행동이 필요하다.                 |
| 4xx | Client Error  | 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없다. |
| 5xx | Server Error  | 서버 오류, 서버가 정상 요청을 처리하지 못했다.            |

#### 1. 2xx - Success

| 상태 코드 | 상태 코드 설명 | 상세 설명                            |
|-------|----------|----------------------------------|
| 200   | OK       | 요청이 정상적으로 처리되었다.                 |
| 201   | Created  | 요청이 정상적으로 처리되었고, 새로운 리소스가 생성되었다. |
| 202   | Accepted | 요청이 접수되었으나 처리가 완료되지 않았다. (대기 상태) |

#### 2. 3xx - Redirection

리다이렉션이란? `Client`가 `Server`에게 `Request`를 전송하였을 때, `Server`가 `Response`로 `3xx` 상태 코드를 전송하면 `Client`는 `Response`
의 `Location` 헤더에 설정된 `URI`로 `Request`를 전송한다.

##### 리다이렉션의 종류

1. 영구 리다이렉션(301, 308) - 특정 리소스의 `URI`가 영구적으로 변경되었을 때 사용한다.
    - `301`은 `GET`으로 요청 메서드가 변경되고, 본문이 제거될 수 있다.
    - `308`은 요청 메서드와 본문을 유지한다.
2. 일시 리다이렉션(302, 307, 303) - 주문 완료 후 주문 내역 화면으로 이동처럼 일시적인 변경이 발생했을 때 사용한다.
    - `302`는 `GET`으로 요청 메서드가 변경되고, 본문이 제거될 수 있다.
    - `307`은 요청 메서드와 본문을 유지한다.
    - `303`은 `302`와 동일하지만, `GET`으로 요청 메서드가 변경 된다.
3. 특수 리다이렉션 - 특수한 상황에서 사용한다.
    - 결과 대신 캐시를 사용한다.

| 상태 코드 | 상태 코드 설명           | 상세 설명                                                                                                          |
|-------|--------------------|----------------------------------------------------------------------------------------------------------------|
| 301   | Moved Permanently  | 리소스의 `URI`가 변경되었으며, 요청 메서드가 `GET`으로 변경하고, 본문이 제거될 수 있다.                                                        |
| 302   | Found              | 리소스의 `URI`가 변경되었으며, 요청 메서드가 `GET`으로 변경하고, 본문이 제거될 수 있다. 본래 의도는 HTTP 메서드를 유지하는 것이지만, 대부분의 브라우저에서는 `GET`으로 변경된다. |
| 303   | See Other          | 리소스의 `URI`가 변경되었으며, 요청 메서드가 `GET`으로 변경된다.                                                                      |
| 307   | Temporary Redirect | 리소스의 `URI`가 변경되었으며, 요청 메서드와 본문을 유지한다. 요청 메서드를 변경하고 싶지 않다면 `307`을 사용한다.                                         |
| 308   | Permanent Redirect | 리소스의 `URI`가 변경되었으며, 요청 메서드와 본문을 유지한다.                                                                          | 

4. 기타 리다이렉션

| 상태 코드 | 상태 코드 설명         | 상세 설명                                                           |
|-------|------------------|-----------------------------------------------------------------|
| 300   | Multiple Choices | 사용하지 않는다.                                                       |
| 304   | Not Modified     | 클라이언트가 이미 가지고 있는 리소스를 요청하였으며, 리소스가 수정되지 않았다. 주로 캐시를 사용할 때 발생한다. |

##### PRG(Post/Redirect/Get) 패턴

`POST`로 데이터를 전송하고, `Response`로 `3xx` 상태 코드를 전송하여 `GET`으로 데이터를 조회하는 패턴이다.
브라우저에서 새로고침(`F5`)은 마지막 요청을 다시 보내는 것이기 때문에, `POST`로 데이터를 전송하고 새로고침을 하면 데이터가 다시 전송된다.
이를 방지하기 위해 `POST`로 데이터를 전송하고, `Response`로 `3xx` 상태 코드를 전송하여 `GET`으로 데이터를 조회하는 패턴을 사용한다.
만약 클라이언트에서 새로고침을 하면, `GET`으로 데이터를 조회하는 `Request`를 전송하게 된다.

#### 3. 4xx - Client Error

| 상태 코드 | 상태 코드 설명     | 상세 설명                                                                                                                                                                                                                |
|-------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 400   | Bad Request  | 클라이언트가 잘못된 요청을 보내었다.                                                                                                                                                                                                 |
| 401   | Unauthorized | 클라이언트가 해당 리소스에 대한 인증이 필요하다.<br/>해당 오류 발생 시, `WWW-Authenticate` 헤더와 함께 인증 방법을 설명해야 한다.<br/>~참고~ 인증(Authentication)은 본인이 누구인지 확인하는 것이고, 인가(Authorization)는 권한을 확인하는 것이다. 오류 메시지가 `Unauthorized`이지만, 인증 되지 않음 (이름이 아쉽다) |
| 403   | Forbidden    | 클라이언트가 해당 리소스에 대한 인가가 필요하다.                                                                                                                                                                                          |
| 404   | Not Found    | 클라이언트가 요청한 리소스가 존재하지 않는다.                                                                                                                                                                                            |

#### 4. 5xx - Server Error

| 상태 코드 | 상태 코드 설명              | 상세 설명                                                           |
|-------|-----------------------|-----------------------------------------------------------------|
| 500   | Internal Server Error | 서버 내부 오류로 인해 요청을 수행할 수 없다.                                      |
| 503   | Service Unavailable   | 서버가 일시적으로 요청을 처리할 수 없다. Retry-After 헤더 필드로 얼마 뒤에 복구되는지 보낼 수 있다. |

##### 4xx vs 5xx

4xx는 클라이언트의, 5xx는 서버의 오류로 인해 요청을 수행할 수 없음을 의미한다.
4xx는 클라이언트가 요청을 잘못 보낸 경우이기 때문에, 클라이언트가 요청을 재시도하면 정상적으로 처리될 수 있지만, 5xx는 서버의 오류로 인해 요청을 수행할 수 없는 경우이기 때문에, 클라이언트가 요청을
재시도하더라도 정상적으로 처리되지 않는다.

### HTTP Header

`HTTP Header`의 특징

- `header-field` = `field-name` ":" OWS `field-value` OWS
    - (`OWS:Optional White Space` - 선택적 공백)
- `field-name`은 대소문자를 구분하지 않는다. (`Host`, `host`, `HOST`는 모두 동일하다.)

#### 1. HTTP Header 구조

##### 1. RFC2616

```header
POST / HTTP/1.1
Host: localhost:8000
User-Agent: Mozilla/5.0 (Macintosh; ...) ... Firefox/51.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
...
Content-Type: multipart/form-data; boundary=---------------------------9051914041544843365972754266
Content-Length: 554

-123124
(more data)
```

- `Header` 분류

| Header 분류       | 설명                     | 예시                                                   |
|-----------------|------------------------|------------------------------------------------------|
| General Header  | 메시지 전체에 적용되는 정보를 제공한다. | Date, Connection, Cache-Control, Transfer-Encoding 등 |
| Request Header  | 요청 정보를 제공한다.           | Host, User-Agent, Accept, Accept-Language 등          |
| Response Header | 응답 정보를 제공한다.           | Location, Server, Content-Encoding 등                 |
| Entity Header   | 엔티티 본문에 대한 정보를 제공한다.   | Allow, Content-Type, Content-Length 등                |

##### 2. RFC723x

1. Entity -> Representation
2. Representation = Representation Metadata + Representation Data

### 표현 Representation

| 표현 Representation | 설명                        |
|-------------------|---------------------------|
| Content-Type      | 표현 데이터의 형식을 나타낸다.         |
| Content-Encoding  | 표현 데이터의 압축 방식을 나타낸다.      |
| Content-Language  | 표현 데이터의 자연 언어를 나타낸다.      |
| Content-Length    | 표현 데이터의 길이를 바이트 단위로 나타낸다. |

표현헤더는 전송(request)과 응답(response) 모두에 사용된다.

#### 1. Content-Type

`Content-Type`이란? 미디어 타입과 문자 인코딩을 나타낸다.
클라이언트에서 서버로 데이터를 전송할 때, `Content-Type`을 통해 데이터의 타입을 알려주고, 서버에서 클라이언트로 데이터를 전송할 때, `Content-Type`을 통해 데이터의 타입을 알려준다.
produces, consumes의 개념이다.

##### 2. Content-Encoding

`Content-Encoding`이란? 데이터의 압축 방식을 나타낸다. 데이터를 전달하는 곳(서버, 클라이언트)에서 압축 후 전송하고, 데이터를 전달 받는 곳(클라이언트, 서버)에서 압축을 해제한다.
ex) gzip, deflate, identity

##### 3. Content-Language

표현 데이터의 자연 언어를 나타낸다. ex) ko, en, en-US

##### 4. Content-Length

표현 데이터의 길이를 바이트 단위로 나타낸다.

### 콘텐츠 협상 Content Negotiation

`Content Negotiation`이란? 클라이언트가 선호하는 표현(Representation)을 요청하는 것을 의미한다.
협상 헤더에는 `Accept`, `Accept-Charset`, `Accept-Encoding`, `Accept-Language`가 있고 요청시에만 사용된다.

| 협상 헤더           | 설명                        |
|-----------------|---------------------------|
| Accept          | 클라이언트가 선호하는 미디어 타입을 알려준다. |
| Accept-Charset  | 클라이언트가 선호하는 문자 인코딩을 알려준다. |
| Accept-Encoding | 클라이언트가 선호하는 압축 인코딩을 알려준다. |
| Accept-Language | 클라이언트가 선호하는 자연 언어를 알려준다.  |

##### 우선순위 Quality Values(q)

우선순위는 `Quality Values(q)`를 사용하여 표현한다. `Quality Values(q)`는 `0 ~ 1` 사이의 실수이며 `q`가 높은 것이 높은 순위를 가지고, `q`가 생략되면 `1`이다.

### 전송 방식

#### 1. 단순 전송

`HTTP`는 기본적으로 단순 전송을 사용한다. 단순 전송이란? `HTTP`는 `TCP`를 기반으로 하기 때문에, `TCP`의 특징인 `3-way handshake`를 통해 연결을 수립하고, `HTTP` 통신을 통해
데이터를 전송하는 것을 의미한다.

#### 2. 압축 전송

`HTTP`는 `Content-Encoding`을 통해 데이터를 압축하여 전송할 수 있다. `Content-Encoding`은 `gzip`, `deflate`, `identity` 등이 있다.

#### 3. 분할 전송

분할 정복을 통해 데이터를 분할하여 전송할 수 있다. `Content-Length`를 사용하지 않고, `Transfer-Encoding`을 사용하여 데이터를 분할하여 전송한다.

#### 4. 범위 전송

`HTTP`는 `Range`를 통해 특정 범위의 데이터를 요청할 수 있다. `Range`는 `Content-Range`와 함께 사용된다.

### 일반 정보

| 일반 정보 General Header | 설명                                                      |
|----------------------|---------------------------------------------------------|
| From                 | 유저 에이전트의 이메일 주소를 나타낸다.                                  |
| Referer              | 이전 웹 페이지의 주소를 나타낸다.(유입 경로) `referer`는 `referrer`의 오타이다. |
| User-Agent           | 유저 에이전트의 애플리케이션 정보를 나타낸다. ex) Mozilla/5.0 ...           |
| Server               | 서버의 소프트웨어 정보를 나타낸다. ex) Apache/2.2.22 ...               |
| Date                 | 메시지가 생성된 날짜를 나타낸다. ex) Tue, 15 Nov 1994 08:12:31 GMT    |

### 특별한 정보

| 특별한 정보 Entity Header | 설명                                                                                                                 |
|----------------------|--------------------------------------------------------------------------------------------------------------------|
| Host                 | 요청한 호스트의 정보를 나타낸다. 하나의 서버가 여러 도메인을 처리하는 경우 혹은 하나의 IP 주소에 여러 도메인이 존재하는 경우, `Host` 헤더를 통해 어떤 도메인으로 요청이 들어왔는지 알 수 있다. |
| Location             | 리다이렉션된 요청의 `URI`를 나타낸다. ex) http://www.w3.org/pub/WWW/                                                             |
| Allow                | 허용되는 요청 메서드를 나타낸다. ex) GET, HEAD, PUT, POST, DELETE, ...                                                           |
| Retry-After          | 서비스가 복구되는 시간을 나타낸다. ex) Retry-After: 120 (초단위)                                                                     |

### 인증

| 인증 Authentication Header | 설명                                                                                                          |
|--------------------------|-------------------------------------------------------------------------------------------------------------|
| Authorization            | 클라이언트 인증 정보를 서버에 전달한다. ex) Authorization: Basic ...                                                         |
| WWW-Authenticate         | 리소스 접근 시 필요한 인증 방법을 서버에서 클라이언트에게 알려준다. `401:Unauthorized`과 함께 사용된다. ex) WWW-Authenticate: Basic realm="..." |

### Cookie

`Cookie`란? 클라이언트의 상태 정보를 저장하고, 관리하기 위해 사용한다. `Cookie`는 `Header:Set-Cookie`와 `Cookie.class`를 사용하여 사용한다. `Cookie`
는 `key=value` 형태로 저장되며, 모두 문자열로 저장된다. 쿠키 정보는 항상 서버에 전달되며 이로 인해 추가 트래픽을 발생시킨다. 또한 클라이언트에 저장되는 특성 때문에 보안에 취약하며, 최소한의 정보만
전달하는 것이 좋다. 서버에 전송하지 않고 웹 브라우저 내부에 데이터를 저장하고 싶다면 `LocalStorage`, `SessionStorage`를 사용한다.

#### 1. Cookie 동작 방식

1. 클라이언트가 `HTTP` 요청을 전송한다.
2. 서버는 `HTTP` 응답을 통해 `Set-Cookie` 헤더를 전송한다.
3. 클라이언트는 `Set-Cookie` 헤더를 전송받으면 `Cookie`를 저장한다.
4. 클라이언트는 `HTTP` 요청을 전송할 때, `Cookie`를 `Cookie` 헤더에 담아 전송한다.
5. 서버는 `Cookie` 헤더를 통해 클라이언트의 `Cookie`를 확인한다.

#### 2. Cookie 생명주기

1. Expires - 만료일이 되면 쿠키를 삭제한다.
2. Max-Age - 쿠키를 생성한 시점으로부터 지정한 시간이 지나면 쿠키를 삭제한다.

`Max-Age`가 `Expires`보다 우선순위가 높으며 `Max-Age` 값을 0이나 음수로 설정하면 쿠키를 삭제한다.

#### 3. Cookie 도메인

`Cookie`는 `Domain`을 기준으로 하위 도메인에도 전송된다. ex) `Domain`이 `example.com`인 경우, `dev.example.com`에도 전송된다. 생략한 경우, `Domain`은 현재
도메인이 된다.

#### 4. Cookie 경로

`Cookie`는 `Path`를 기준으로 하위 경로에도 전송된다. ex) `Path`가 `/`인 경우, `/example`에도 전송된다.

#### 5. Cookie 보안

`Cookie`는 `Secure`를 통해 `HTTPS`로만 전송되도록 설정할 수 있다. `HttpOnly`를 통해 `JavaScript`에서 `Cookie`에 접근할 수 없도록 설정할 수 있다. `SameSite`를
통해 `Cross-Site`로 쿠키가 전송되는 것을 방지할 수 있다.

### Cache

`Cache`란? `HTTP` 통신 시, `Cache`를 통해 응답을 캐싱하여 불필요한 데이터 전송을 줄일 수 있다. `Cache`는 `Cache-Control` 헤더를 통해 사용한다.

#### 1. Cache-Control

`Max-Age`를 통해 캐시의 유효 시간을 설정할 수 있다. `Cache-Control`은 `Request`와 `Response` 모두에 사용된다. 캐시 유효 시간이 초과하면, 서버에 재요청하여 캐시를 갱신한다.
이때 네트워크 다운로드가 또다시 발생한다.

#### 검증 헤더와 조건부 요청

`Cache`는 `ETag`와 `Last-Modified`를 통해 캐시를 검증한다. `ETag`는 `Entity Tag`의 약자로, `Entity`의 `hash` 값을 의미한다. `Last-Modified`
는 `Entity`의 마지막 수정 시간을 의미한다. `ETag`와 `Last-Modified`는 `Response`에 사용된다. `If-None-Match`와 `If-Modified-Since`는 `Request`에
사용된다.

#### 캐시와 조건부 요청 헤더

| 캐시 헤더                                 | 설명                                                                                                                                                                           |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cache-Control                         | 캐시 지시어(directives)를 통해 캐시 동작을 설정한다.<br/>ex) Cache-Control: max-age=60,<br/>Cache-control: no-cache (데이터는 캐시하지만, 검증을 위해 서버에 요청),<br/>Cache-control: no-store (데이터를 캐시하지 않는다.) |
| Pragma                                | 캐시 동작을 설정한다. `Cache-Control`과 동일하다. HTTP 1.0 하위 호환성을 위해 사용된다.                                                                                                                | 
| Expires                               | 캐시 만료 시간을 설정한다. `Cache-Control`의 `max-age`와 동일하다. HTTP 1.0 하위 호환성을 위해 사용된다.                                                                                                  |
| ETag                                  | 캐시용 데이터에 대한 `hash` 값을 설정한다. `ETag`는 `Entity Tag`의 약자이다.                                                                                                                      |
| Last-Modified                         | 캐시용 데이터의 마지막 수정 시간을 설정한다.                                                                                                                                                    |
| If-Match, If-None-Match               | `ETag` 값을 통해 캐시를 검증한다. `ETag`가 동일하면, 캐시를 사용한다.                                                                                                                               |
| If-Modified-Since, If-Unodified-Since | `Last-Modified` 값을 통해 캐시를 검증한다. `Last-Modified`가 동일하면, 캐시를 사용한다.                                                                                                             |

### 프록시

`Proxy`란? 클라이언트와 서버 사이에서 중계기로 동작한다. `Proxy`는 `Cache`를 사용하여 불필요한 데이터 전송을 줄일 수 있다. 물리적으로 거리가 먼 클라이언트와 서버 사이에서 데이터를 전송할 때,
중간에 `Proxy`를 두어 데이터를 캐싱하고, `Proxy`가 데이터를 전송하는 것이 더 효율적이다.(CDN: Content Delivery Network)

### 캐시 무효화

`Cache`는 `Cache-Control` 헤더를 통해 캐시를 무효화할 수 있다. `Cache-Control` 헤더에 `no-cache, no-store, must-revalidate`를 설정하면 캐시를 무효화할
수 있다.
