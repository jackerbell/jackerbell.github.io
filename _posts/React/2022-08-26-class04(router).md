---
categories: Coding	
tag: react
---



# 2022. 08. 25. 수업내용 정리 #

## Router 구현..  (코드 설명 위주로)

<br>

1. Router

   사용자가 요청한 URL에 따라 맞는 페이지를 보여주는 것

   이번 포스트에서는 리액트에서 라우팅 관련 라이브러리 중 가장 범용적으로 쓰이는 리액트 라우터(`react-router-dom`)을 사용합니다. 

   리액트 라우터는 사용자가 입력한 주소를 감지하는 역할을 하며, 여러 환경에서 동작할 수 있도록 여러 종류의 라우터 컴포넌트를 제공합니다. 

   이 중 가장 많이 사용되는 라우터 컴포넌트는 BrowserRouter(HTML5를 지원하는 브라우저의 주소를 감지)와 HashRouter(해시주소를 감지)입니다.

   이번 포스트에서는 BrowerRouter,Routes,Route를 사용합니다.

   <br><br>

2. 설치

   1. npm

   ```react	
   npm install react-router-dom
   ```

   <br>

   2. yarn

   ```react
   yarn add react-router-dom
   ```

   <br><br>

3. 예시

   App.js

   ```react
   import React, { Component } from 'react';
   import { BrowserRouter, Routes, Route } from 'react-router-dom';
   import Header from './Header';
   import Main from './Main';
   import Product from './Product';
   
   const App = () => {
   	return (
   		<div className='App'>
   			<Header exact path='/'> <!-- 주소가 겹치지 않도록('/') exact path로 설정 -->
   			<Main path='/main'>
   			<Product path='/product'>
   		</div>
   	);
   }
   
   export default App;
   ```

   <br>

   Header.js

   ```react
   import React from 'react';
   
   function Header(props) {
       return (
   		<>
   			<h1>헤더입니다.</h1>
   		</>
       );
   }
   
   export default Header;
   ```

   <br>

   Main.js

   ```react
   import React from 'react';
   const Main = (props) => {
   	return (
   		<>
   			<h3>안녕하세요. 메인페이지 입니다.</h3>
   		</>
   	);
   };
   
   export default Main;
   ```

   Product.js

   ```react
   import React from 'react';
   
   const Product = (props) => {
       return (
           <>
               <h3>상품 페이지입니다.</h3>
           </>
       );
   }
   
   export default Product;
   출처: https://goddaehee.tistory.com/305 [갓대희의 작은공간:티스토리]
   ```

   <br>

   웹페이지 화면 ▼

   ![router](../../images/2022-08-26-class04(router)/router.png)

4. 응용

   App.js

   ```react
   
   import {Component} from 'react'
   import {BrowserRouter,Routes,Route} from 'react-router-dom';
   import Home from './components/Home.js';
   import Search from './components/Search.js';
   import InputComp from './components/InputComp.js';
   
   import './App.css';
   
   class App extends Component{
   
     constructor(props){
       super(props)
       this.state={
   
       }
     }
   
     render(){
       return(
         <div id='app'>
             <BrowserRouter> <!-- HTML5상에서 라우터 기능 사용이 가능하도록 해줌 -->
                 <InputComp/>
                 <Routes> <!-- 여러 개의 Route가 필요할 때, 사용-->
                     <Route exact path='/' element={<Home/>}/> <!--라우팅할 요소들을 각각 넣어줌..  -->
                     <Route path='/search' element={<Search/>}/>
                 </Routes>
             </BrowserRouter>
         </div>
       )
     }
   }
   
   export default App;
   ```

   <br>

   App.css

   ```css
   #app{
     width:1000px;
     height:1000px;
     background-color:aqua;
     margin:0 auto;
   }
   ```

   <br>

   Home.js

   ```react
   import {Component} from 'react'
   import '../css/Home.css'
   
   class Home extends Component{
   
     constructor(props){
       super(props)
       this.state={
   
       }
     }
   
     render(){
       return(
         <div id='home'>
               홈
         </div>
       )
     }
   }
   
   export default Home;
   ```

   <br>

   Home.css

   ```css
   #home{
       width:100%;
       height:500px;
       background-color: blue;
   }
   ```

   <br>

   웹페이지 화면(다른 요청이 없으므로 default인 Home 컴포넌트가 나옴) ▼

   ![image-20220826214003667](../../images/2022-08-26-class04(router)/image-20220826214003667.png)

   <br>

   단순히 주소창(URL)에 해당 라우터의 경로를 입력하는 것이 아니라 HTML내부의 입력(input)요소를 통해 검색어(URL요청)를 입력하고 검색버튼을 눌러 페이지를 전환하는 방식으로 해보겠습니다. <br>

   InuptComp.js

   ```react
   import {Component} from 'react'
   import '../css/InputComp.css'
   
   class Search extends Component{
   
     constructor(props){
       super(props)
       this.state={
           searchText:''
       }
     }
   
     searchBook=()=>{
       alert('책검색!')
       //window.location.href='/search?searchText='+this.state.searchText
       window.location.href=`/search?searchText=${this.state.searchText}&display=10&country=JPN`
       //location객체의 hyper reference
     }
   
     inputChange=(e)=>{//이벤트객체 정보가 매개변수에 e에 넘어온다.
           //console.log('change!')
           //console.log(e.target.value)
           this.setState({
               searchText:e.target.value
           })//입력창에서 읽어들인 검색어 저장
     }
   
     render(){
       return(
         <div id='input-comp'>
             <input type='text' placeholder='검색어' 
             onChange={this.inputChange}/><!-- input의 value값이 바뀌었으므로 -->
             <button onClick={this.searchBook}>검색</button>
         </div>
       )
     }
   }
   
   export default Search;
   ```

   <br>먼저 input에 value값을 받아올 `searchText`라는 state를 생성하고 `inputChane`함수를 onChange 이벤트에 등록합니다. <br>

   그 후 input에 입력한 값을 읽어들여 state에 저장합니다.<br>

   최종적으로  검색 버튼을 눌러 onClick 이벤트에 등록된 `searchBook`함수로 URL요청을 보냅니다.<br>

   이 때, windwo 객체의 loacation.href는 location 객체에 속한 프로퍼티로 현재 접속중인 페이지의 정보를 갖고 있습니다. <br>

   또한 값을 변경할 수 있는 프로퍼티이기 때문에 다른 페이지로 이동하는데도 사용되고 있습니다. <br><br>

   라우터에서는 path 뒤에 query string을 받아서 동작을 바꿔야하는 경우가 있습니다. <br>

   여기서 query string이란 사용자가 입력 데이터를 전달하는 방법중의 하나로, url 주소에 미리 협의된 데이터를 파라미터를 통해 넘기는 것을 의미합니다.<br>

   이러한 과정을 보다 쉽게 하기 위해 리액트의 `query-string` 모듈에서 `queryString`객체를 사용합니다. <br>

   위의 예시에서도 `/search?searchText=${this.state.searchText}&display=10&country=JPN`의 URL에 요청을 보내는 것을 확인할 수 있습니다. <br>

   Search.js

   ```react
   import {Component} from 'react'
   import '../css/Search.css'
   import queryString from 'query-string';
   //import axios from 'axios';
   //'axios'모듈에서 axios함수를 가져온다
   class Search extends Component{
   
     constructor(props){
       super(props)
       this.state={
   
       }
     }
   
     componentDidMount(){
       //초기화작업,네트워크를 통한 데이터 요청,서버에 데이터요청
       //ex)네이버 검색 API : naver.api.com/movie.json?query='스파이더맨'
       console.log('Search')
       console.log('window.location',window.location)//href,hostname,pathname~~~
       console.log('window.location.href',window.location.href)//http://localhost:3000/search?searchText=sdfsdf
       console.log('window.location.search',window.location.search)//?searchText=sdfsdf
       const queryObj=queryString.parse(window.location.search)
       console.log(queryObj)//{country:"JPN",display:"10",searchText:'hello'}
       console.log(queryObj.searchText)//'hello'
       const searchText=queryObj.searchText
       //http://www.naver.api.com/search/movie.json?query=searchText
       //날려서 데이터 응답 받기
   
       //JSON.parse
       //XmlHttpRequest
       //$.ajax
   
       //파싱해서 search안에 검색어만 뽑아냄
       //검색어를 알아낸 후 그 검색어로 네이버 검색 API에 요청 보내서 데이터 받아옴.
       //받아와서 state에저장
     }
   
     render(){
       return(
         <div id='search'>
             검색
         </div>
       )
     }
   }
   
   export default Search;
   ```

   <br>window.location.href가 구체적으로 어떤 것을 나타내는 지 확인해보기 위해서 

   console로 각각이 나타내는 것들을 확인해보았습니다. <br>

   웹페이지 화면(검색어 입력 후 전송) ▼

   ![router](../../images/2022-08-26-class04(router)/router-166152639663012.png)

   <br>

   URL 요청 전송 후 전환된 화면 및 바뀐 URL ▼

   ![router](../../images/2022-08-26-class04(router)/router-166152658888214.png)

   <br>

   개발자도구의 콘솔창 ▼

   ![router](../../images/2022-08-26-class04(router)/router-166152683422316.png)

   