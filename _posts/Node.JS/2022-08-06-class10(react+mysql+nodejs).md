---
categories: Coding	
tag: Node.js
toc: true
---



# 2022. 08. 04. 수업내용 정리 #

## react+mysql+nodejs 연동 with axios

<br>

* react + mysql + nodejs + axios

  1. 프로젝트 폴더 생성(사전에 node js 설치 필요)

     > npx create-react-app {project name} (cmd 창에 그대로 입력)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-16597830890072.png)

     <br>

  2. App.js 파일에서 클래스형 컴포넌트 생성 및 App.css 작성 defalut code 제거(App.js, App.css)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-16597854262394.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979058621116.png)

     <br>

  3. src 폴더에 server 폴더 생성 후 server.js 파일 생성, 이후 express 설치 및 기본 코드 작성하고 <br>
     server 폴더 내부에 config폴더 생성 및 내부에 db.js파일 생성까지 진행

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-16597859467306.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165978985738412.png)

     ![image-20220806214457936](../../images/2022-08-06-class09(react+mysql+nodejs)/image-20220806214457936.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-16597859765068.png)

     <br>

  4. axios, mysql, body-parser 도 설치합니다. 이후 필요한 요청을 추가합니다.

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165978877702510.png)

     <br>

  5.  package.jason에 "proxy":"http://localhost:4000"추가 요청을 보낼 주소를 설정

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979011541514.png)

     <br>

  6. 터미널 2개로 split 하여 왼쪽은 서버 실행, 오른쪽은 클라이언트(리액트)실행 후 동작되는지 확인합니다.

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979102594118.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979106785820.png)

     <br>

  7. App.js 안에 axios 요청 추가, get, post, put, delete 등등 상세요청 작성합니다.

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979200400026.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979153000622.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979156933224.png)

     <br>

  8. axios.get(클라이언트) -> app.get(서버) -> db.query(DBMS) 로 DB값 출력도 확인하여 동작상태를 점검합니다.<br>

     axios.get(클라이언트) -> app.get(서버) -> db.query(DBMS) 로 DB값 출력도 확인한다.

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979224628628.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979229758830.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979247456432.png)

     ![모두연동](../../images/2022-08-06-class09(react+mysql+nodejs)/모두연동-165979256913934.png)

  9. 

     

  

​	