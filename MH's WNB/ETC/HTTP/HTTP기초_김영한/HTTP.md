# IP
1. Internet Protocol
2. IP protocol의 한계
	1) 비연결성 : 패킷을 받을 대상이 없거나 받을 수 있는 상태가 아니어도 패킷 전송
	2) 비신뢰성 : 중간에 패킷이 사라지거나, 순서대로 전송X
	3) 프로그램 구분 : 같은 IP 서버에 통신하는 application이 여럿일 때

[[인터넷 프로토콜 스택 4계층]]
# TCP
1. 전송 제어 프로토콜(Transmission Control Protocol)
2. 신뢰할 수 있는 프로토콜로 현재 대부분 TCP 사용
3. [[PORT]] 정보가 있어서 어떤 애플리케이션에 대한 응답인지 찾아갈 수 있음
4. 특징
	1) 연결 지향 : TCP 3way handshake(가상 연결)
	2) 데이터 전달 보증
	3) 순서 보장

# UDP
1. 사용자 데이터그램 프로토콜(User Datagram Protocol)
	1) 기능이 거의 없음
	2) 3 way handshake X
	3) 데이터 전달 보증 X
	4) 단순하고 빠름
	5) 유튜브를 생각하면 됨
	6) IP + PORT + 체크섬 정도로 생각하면 됨
	7) 애플리케이션 추가 작업 필요

# DNS
1. Domain Name System
2. 도메인명을 IP주소로 변환 (like 전화번호부)

# URI
1. Uniform Resource Identifier : 리소스를 식별하는 통일된 방식
2. URI = <u>URL</u>(Resource Locator) + <u>URN</u>(Resource Name)
3. example
	1) schema://\[userinfo@]host\[:port]\[/path]\[?query]\[\#fragment]
	2) \https://www.google.com:443/search?q=hello&hl=ko

# 웹브라우저의 요청 흐름
1. 웹 브라우저가 HTTP 메세지 생성
	> GET /search?q=hello&hl=ko HTTP/1.1
	> HOST: \www.google.com
1. SOCKET 라이브러리를 통해 전달
	1) TCP/IP 연결
	2) 데이터 전달
2. TCP/IP 패킷 생성, HTTP 메세지 포함

---

# HTTP
- HyperText Transfer Protocol
- HTTP 메세지에 모든 것을 전송 가능(HTML, TEXT, Image, 음성, 영상, JSON, XML 등 거의 모든 형태의 데이터 전송 가능)
- 기반 프로토콜
	- TCP : HTTP/1.1(현재 많이 사용), HTTP/2
	- UDP : HTTP/3
- **HTTP 특징**
	- Client Server 구조
		- Request, Response 구조
		- client -> server 요청 보내고 응답 대기함
		- client <- server 요청에 대한 결과를 응답함
		- client(UI등), server(복잡한 비즈니스 로직에 집중) 각각 독립적으로 진화 가능
	- 무상태 프로토콜(Stateless) 지향
		- 어떤 내용을 주고받았는지 server가 알지 못함(이전 문맥을 모름)(이전 문맥을 아는 것은 Stateful)
		- 서버의 무한한 증설이 가능(어떤 서버던 응답이 정상적으로 가능하므로..)
		- server가 client의 상태 보존X
			- 장점 : 서버 확장성 좋음(스케일 아웃 - 수평 확장에 유리)
			- 단점 : 클라이언트가 추가 데이터 전송해야 함(보낼 데이터 양이 많음)
		- 로그인 기능의 경우에는 상태를 유지해야 함(브라우저 쿠키, 서버 세션 등을 사용하여 상태 유지) 
	- 비연결성
		- 최소한의 자원만 사용(서버 자원을 효율적으로 사용 가능)
		- 한계
			- TCP/IP 연결을 매번 해야 함(3 way handshake 시간 소요)
			- 웹 브라우저로 사이트를 요청하면 HTML, JS, CSS, IMG등 많은 자원이 함께 다운로드
			- 현재 HTTP 지속 연결(Persistent Connections)로 문제 해결
			- HTTP/2, HTTP/3에서 많은 최적화가 이루어짐
	- HTTP 메세지로 통신
		- 구조
			- start-line 시작 라인
			- header 헤더 (meta data들 있음)
			- empty line 공백 라인(CRLF)
			- message body
	- 단순함, 확장 가능

---

# HTTP 메서드
- URI 설계
	- 리소스(명사) 식별이 중요
	- 행위(동사)는 분리
- 종류
	- **GET**: 리소스 조회
	- **POST**: 요청 데이터 처리, 주로 등록에 사용
	- **PUT**: 리소스를 대체함. 해당 리소스가 없으면 생성(폴더에 파일 복사하는 것과 비슷, 리소스 위치를 알고 있다는 점에서 POST와 다름)
	- **PATCH**: 리소스 부분 변경
	- **DELETE**: 리소스 삭제
	- HEAD: GET과 동일하지만 메세지 부분을 제외하고 상태 줄과 헤더만 반환
	- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드) 설명(주로 CORS에서 사용)
- 속성
	- 안전(Safe Methods): 호출해도 리소스 변경X
	- 멱등(Idempotent Methods)
		- 얼마나 호출하든 결과가 같음
		- 자동 복구 메커니즘 사용 가능(여러번 호출해도 결과는 같으니까)
		- 외부 요인으로 중간에 리소스가 변경되는 것은 고려하지 않음
	- 캐시가능(Cacheable Methods)
		- GET, HEAD, POST, PATCH가 캐시 가능하지만 실제로는 GET, HEAD만 캐시로 사용
- 활용
	- Client -> Server 데이터 전송
