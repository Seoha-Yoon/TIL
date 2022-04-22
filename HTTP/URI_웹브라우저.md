# URI와 웹 브라우저 요청 흐름

## URI (Uniform Resource Identifier)

* Uniform 리소스를 식별하는 통일 된 방식)
  
  Resource (자원)
  
  Identifier (다른 항목과 구분하는데 필요한 정보)

* URI = URL (Uniform Resource Locator - 위치) + URN (Uniform Resource Name - 이름)

### URL 문법

scheme://[userinfo@]host[:port][/path][?query][#fragment]

https://www.google.com:443/search?q=hello&hl=ko

* **scheme**
  
  프로토콜  : 어떤 방식으로 자원에 접근할 것인가. (https, http, ftp)
  
  https는 http에 보안 추가, 포트는 생략 가능

* **호스트 명**: 도메인명, IP 주소 (www.google.com)

* **포트번호**: 생략 가능 (443)

* **패스**: 리소스 경로 (/search)

* **쿼리 파라미터** (q=hello&hl=ko)
  
  * key = value 형태
  
  * ?로 시작, &로 추가, 문자 형태

* **fragment**: html 내부 북마크 등, 서버에 전송하지 않음



## 웹 브라우저 요청 흐름

https://www.google.com:443/search?q=hello&hl=ko

1. 호스트 명에 따른 DNS 조회 -> IP 주소 get

2. HTTP 요청 메시지 생성
   
   ```
   GET /search?q=hello&hl=ko HTTP/1.1(HTTP 버)
   Host: www.google.com
   ```

3. SOCKET 라이브러리를 통해 전달.

4. TCP/IP 패킷 생성 및 구글 서버에 전송

5. HTTP 응답 메시지 생성
   
   ```
   HTTP/1.1 200 OK
   Content-Type: text/html;charset=UTF-8
   Content-Length: 3423
   
   <html>
       <body>...</body>
   </html>
   ```

6. 웹 브라우저에 응답 패킷 전송 및 웹브라우저에 도착

7. 웹 브라우저 HTML 렌더링


