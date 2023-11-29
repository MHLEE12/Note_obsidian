- Javascript를 브라우저 외에서도 작동할 수 있게 만든 것. chrome의 V8을 이용해 만듦.

### 특징
- Event-driven
- Non-blocking I/O
	- 요청 모두 받음 -> 처리 속도 빠른 것 먼저 처리함(요청이 많거나 오래걸리는 요청이 있어도 멈추거나 대기 시간X )
- 코드가 짧고 쉬워서 빠른 개발 가능

### Setting 
- 버전 확인 : (window) cmd 창에서 > node -v  
- 실행(js 코드를 실행할 수 있음) : > node  + enter 
- npm : 라이브러리 설치를 도와주는 도구
	- npm init : package.json 파일 생성됨
	- npm install express : express 라이브러리 설치
		- 설치하면 package.json 파일 내에 "dependencies" 에 설치한 라이브러리가 추가로 기록된다.
- npm install이 되지 않는다면 yarn 을 검색할 것(명령어가 다르긴 한데 yarn을 npm처럼 사용 가능)

### folder 구성
- node_modules : 라이브러리 설치하면 생기는 폴더. 라이브러리와 관련된 파일을 있음.

### 실행
- 터미널에서 > node \[package.json에서 main 으로 설정한 파일명] 