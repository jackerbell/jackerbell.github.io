---
categories: Coding	
tag: react
---



# 2022. 08. 19. 수업내용 정리 #

## PagiNation 구현..  (코드 설명 위주로)

<br>

1. 주제

   다수의 데이터가 있을 경우 모든 데이터를 한 화면에서 보여주기 힘들경우 페이지를 나누어 보여줄 수 있는 `PagiNation`기능을 구현해 문제를 해결할 수 있습니다.<br>

   ```react
   import './App.css';
   import { Component } from 'react';
   
   
   class App extends Component {
   
     constructor(props){
       super(props)
       this.state={
           //사용할 데이터
           postList:[
             {no:10,title:'title-10',contents:'contents-10',author:'kim',writeDate:'2022-08-30'},
             {no:9,title:'title-9',contents:'contents-9',author:'lee',writeDate:'2022-07-30'},
             {no:8,title:'title-8',contents:'contents-8',author:'park',writeDate:'2022-06-30'},
             {no:7,title:'title-7',contents:'contents-7',author:'choi',writeDate:'2022-05-30'},
             {no:6,title:'title-6',contents:'contents-6',author:'son',writeDate:'2022-04-30'},
             {no:5,title:'title-5',contents:'contents-5',author:'sin',writeDate:'2022-03-30'},
             {no:4,title:'title-4',contents:'contents-4',author:'kang',writeDate:'2022-02-30'},
             {no:3,title:'title-3',contents:'contents-3',author:'jang',writeDate:'2022-01-30'},
             {no:2,title:'title-2',contents:'contents-2',author:'oh',writeDate:'2021-12-30'},
             {no:1,title:'title-1',contents:'contents-1',author:'kwon',writeDate:'2021-11-30'},
           ]
       }
     }
   
     render(){
       return (
         <div id='app'>
           <PostList postList={postList}/>
           <PagiNation/>
         </div>
       );
     }
   }
   
   export default App;
   
   ```

   ```css
   #app{
     width:1000px;
     height:1000px;
     background-color: aqua;
     margin:0 auto; 
   }
   ```

   <br><br>

2. 필요한 컴포넌트 생성

   게시글을 나타낼 `Post.js`,  `Post.js`를 `array.map`함수를 이용해서 데이터의 길이만큼 반복적으로 생성해주기 위한 `PostList.js`,  최종적으로<br>

   한 페이지당 게시글 수를 지정하고 iindex 버튼을 누를때마다 해당 페이지로 이동하는 `PagiNation.js`를 추가합니다. <br>

   ```react
   /* PagiNation.js */
   
   import '../css/PagiNation.css';
   import { Component } from 'react';
   
   class PagiNation extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     
   
     render(){
   
       
       return (  
         <div id='pagination'>
            <div>
               총 글 갯수:
             </div>
             <div>
               페이지당 글 갯수:
             </div>
             <div>          
             </div>
         </div>
       );
     }
   }
   
   export default PagiNation;
   ```

   ```css
   /* PagiNation.css */
   
   #pagination{
       width:90%;
       height:100px;
       background-color: brown;
   }
   
   /* 총 페이지수, 페이지당 글 개수, 페이지네이션 박스 자리 */
   #pagination>div:first-child{
       background-color: darkkhaki;
   }
   #pagination>div:nth-child(2){
       background-color: darkmagenta;
   }
   #pagination>div:nth-child(3){
       background-color: darkolivegreen;
   }
   
   ```

   ```react
   /* post.js */
   
   import '../css/Post.css';
   import { Component } from 'react';
   
   class Post extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     render(){
       return (
         <div id='post'>
               <span>
                   {this.props.no}
               </span>
               <span>
                   {this.props.title}
               </span>
               <span>
                   {this.props.author}
               </span>
               <span>
                   {this.props.writeDate}
               </span>
         </div>
       );
     }
   }
   
   export default Post;
   ```

   ```css
   /* Post.css */
   
   #post{
       width:90%;
       height:50px;
       background-color: chartreuse;
       margin:10px;
   }
   #post>span{
       text-align: center;
       padding-top:10px;
       box-sizing: border-box;
   }
   #post>span:first-child{
       float:left;
       width:5%;
       height:100%;
       background-color: darkkhaki;
   }
   #post>span:nth-child(2){
       float:left;
       width: 30%;
       height:100%;
       background-color: darkolivegreen;
   }
   #post>span:nth-child(3){
       float:left;
       width: 15%;
       height:100%;
       background-color: darkmagenta;
   }
   #post>span:nth-child(4){
       float:left;
       width: 15%;
       height:100%;
       background-color: darkorange;
   }
   ```

   ```react
   /* PostList.js */
   
   import '../css/PostList.css';
   import { Component } from 'react';
   import Post from './Post.js';
   
   class PostList extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     render(){
   	// 데이터 나열 1~10
       const result=this.props.postList.map(
           (data)=>(<Post key={data.no} 
               no={data.no} title={data.title} author={data.author}
               writeDate={data.writeDate}/>)
       )
   
       return (
         <div id='post-list'>
           {result}
         </div>
       );
     }
   }
   
   export default PostList;
   
   
   ```

   웹페이지 화면 ▼

   ![image-20220820230828619](../../images/2022-08-19-class03(pagination)/image-20220820230828619.png)

   <br><br>

3. 페이지네이션 index 만들기

   우선 데이터 정보가 한 페이지 안에 모두 나타나고 있으므로 페이지당 일정 갯수만큼 나타내기 위해서 페이지당 목록개수를 설정해야합니다.<br>
   그와 동시에 제대로 나뉘었는지 확인하기 위해서는 각 페이지로 이동해서 확인해야 하므로 각 페이지(위의 경우 1~4)를 나타내는 PagiNation 박스를 하단의 갈색영역에 생성한 후 현재 페이지로 이동하는 함수를 생성해 클릭이벤트로 전달해줍니다. <br>

   `App.js`컴포넌트에서 state에 `postListPerPage:3`,`currentPage:1`을 각각 추가해줍니다. <br>
   그 후 `PagiNation.js`컴포넌트에 페이지네이션 기능에 필요한 데이터의  전체길이:`postList.length`, 페이지당 글 갯수:`postListPerPage`와
   현재페이지 설정을 위해 필요한 현재페이지:`currentPage`를 전달해줍니다. <br>

   먼저 페이지당 데이터를 나누고 이동할 페이지네이션 인덱스를 생성한 후 페이지 이동 기능을 추가합니다.<br>

   ```react
   /* App.js */
   
   import './App.css';
   import { Component } from 'react';
   
   
   class App extends Component {
   
     constructor(props){
       super(props)
       this.state={
           postList:[
             {no:10,title:'title-10',contents:'contents-10',author:'kim',writeDate:'2022-08-30'},
             {no:9,title:'title-9',contents:'contents-9',author:'lee',writeDate:'2022-07-30'},
             {no:8,title:'title-8',contents:'contents-8',author:'park',writeDate:'2022-06-30'},
             {no:7,title:'title-7',contents:'contents-7',author:'choi',writeDate:'2022-05-30'},
             {no:6,title:'title-6',contents:'contents-6',author:'son',writeDate:'2022-04-30'},
             {no:5,title:'title-5',contents:'contents-5',author:'sin',writeDate:'2022-03-30'},
             {no:4,title:'title-4',contents:'contents-4',author:'kang',writeDate:'2022-02-30'},
             {no:3,title:'title-3',contents:'contents-3',author:'jang',writeDate:'2022-01-30'},
             {no:2,title:'title-2',contents:'contents-2',author:'oh',writeDate:'2021-12-30'},
             {no:1,title:'title-1',contents:'contents-1',author:'kwon',writeDate:'2021-11-30'},
           ],
           postListPerPage:3,
           currentPage:1
       }
     }
      
      setCurrentPage=(page)=>{
       alert("페이지설정(App.js):"+page)
       this.setState({
         currentPage:page
       })
       //PagiNation컴포넌트에서 클릭된 
       //페이지번호를 넘겨받아서
       //현재 페이지 번호로 설정한다.
     }
   	
     // 페이지당 데이터 분할
     currentPostList=(postList)=>{
       //slice 메서드 (배열 추출)
       const {currentPage,postListPerPage}=this.state
       //1,3 | 2,3 | 3,3 | 4,3
       //const indexOfLast = currentPage*postListPerPage//1*3->3 , 2*3->6 , 3*3->9 , 4*3->12
       //const indexOfFirst = indexOfLast-postListPerPage//3-3->0 , 6-3->3 , 9-3->6 , 12-3->9
       //const slicePostList=postList.slice(indexOfFirst,indexOfLast)
       //slice(0,3) - 배열 0,1,2 인덱스번호 가진채로 반환 (길이3인 배열)
       //slice(3,6) - 배열 3,4,5 인덱스번호 가진채로 반환 (길이3인 배열)
       //slice(6,9) - 배열 6,7,8 인덱스번호 가진채로 반환 (길이3인 배열)
       //slice(9,12) - 배열 9 인덱스번호 가진채로 반환 (길이3인 배열)
       //indexOfFirst부터 구하고,indexOfLast구하기
       //1페이지 0,0+3
       //2페이지 3,3+3
       //3페이지 6,6+3
       //4페이지 9,9+3
       const indexOfFirst=(currentPage-1)*postListPerPage
       const indexOfLast=indexOfFirst+3 
       const slicePostList=postList.slice(indexOfFirst,indexOfLast) 
       return slicePostList;
     }
       
       
     render(){
       const {postList,postListPerPage,currentPage}=this.state
       return (
         <div id='app'>
           <PostList postList={this.currentPostList(postList)}/><!-- 페이지당 분할해서 보여줌 -->
             <PagiNation postListLength={postList.length}
             postListPerPage={postListPerPage}   
             currentPage={currentPage}
             setCurrentPage={this.setCurrentPage}/>
         </div>
       );
     }
   }
   
   export default App;
   
   ```

   ```react
   /* PagiNation.js */
   
   import '../css/PagiNation.css';
   import { Component } from 'react';
   
   class PagiNation extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     setCurrentPage=(page)=>{//이 때 page는 mapping 과정에서 data로 전달되는 PagiNation Index를 받음.
       //alert("페이지번호 클릭됨!")
       alert(page+"페이지 클릭!")
       this.props.setCurrentPage(page)
       //App.js의 setCurrentPage함수
     }
   
   
     render(){
   
       const {postListLength,postListPerPage}=this.props
       //10,3
       //3,3,3,1 - 1페이지~4페이지, 10/3 -> 3.33 -> 4
       let pageNumbers=[];//페이지 번호가 들어갈 배열
       console.log(postListLength)//10
       console.log(postListPerPage)//3
       const lastPageNum=Math.ceil(postListLength/postListPerPage)//4
       for(var i=1; i<=lastPageNum; i++){//1~4
         pageNumbers.push(i)//1,2,3,4
       }
       console.log(pageNumbers)//[1,2,3,4]
   
       const pageList=pageNumbers.map(
         (data)=>(<span className='page' key={data} // 데이터의 개수를 총 길이만큼 분할한 후 지정된 페이지만 보여줌.
         onClick={()=>this.setCurrentPage(data)}>{data}</span>) //이 때 {}를 없애고 작성해야 바로 호출되지 않고 전달됨.
       )
       //this.setCurrentPage(data)
   
       return (  
         <div id='pagination'>
             <div>
               총 글 갯수:{postListLength}
             </div>
             <div>
               페이지당 글 갯수:{postListPerPage}
             </div>
             <div>
               {pageList}
             </div>
         </div>
       );
     }
   }
   
   export default PagiNation;
   ```

   웹페이지 화면 ▼(1페이지)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166100823985128.png)

   웹페이지 화면 ▼(2페이지 이동)

   ![image-20220821001158068](../../images/2022-08-19-class03(pagination)/image-20220821001158068.png)![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166100835934630.png)

   <br>

   위와 같이 페이지네이션 기능을 확인한 후 이전과 다음으로 이동하는 기능도 추가해줍니다. <br>

   `PagiNation.js`컴포넌트로 이동해 생성해줍니다.<br>

   ```react
   import '../css/PagiNation.css';
   import { Component } from 'react';
   
   class PagiNation extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     setCurrentPage=(page)=>{
       alert(page+"페이지 클릭!")
       this.props.setCurrentPage(page)
     }
   
     prevPage=()=>{
       const {currentPage,setCurrentPage} = this.props
       if(currentPage === 1){// 첫번째 페이지에서 이전 페이지로 이동 방지
         alert('이동불가!')
         return  // 강제 종료
       }
       else{ //이동 가능한 경우 현재 페이지의 인덱스에서 1을 감소시킨 후 setCurrentPage에 삽입.. 
         const prevPage = currentPage - 1 
         setCurrentPage(prevPage)
       }
     }
   
     nextPage=()=>{
       const {currentPage,setCurrentPage,postListLength,postListPerPage} = this.props
       const endIndex = Math.ceil(postListLength/postListPerPage) //현재 예시의 경우 3.3333.. → 4로 올림.
       if( currentPage === endIndex){ //마지막 인덱스일 때 다음으로 이동불가
         alert('이동불가!')
         return // 강제종료
       }
       else{ //이동 가능한 경우 현재 페이지의 인덱스에서 1을 증가시킨 후 setCurrentPage에 삽입.. 
         const nextPage = currentPage + 1
         setCurrentPage(nextPage)
       }
     }
   
     render(){
   
       const {postListLength,postListPerPage}=this.props
       let pageNumbers=[];
       console.log(postListLength)
       console.log(postListPerPage)
       const lastPageNum=Math.ceil(postListLength/postListPerPage)
       for(var i=1; i<=lastPageNum; i++){
         pageNumbers.push(i)
       }
       console.log(pageNumbers)
   
       const pageList=pageNumbers.map(
         (data)=>(<span className='page' key={data}
         onClick={()=>this.setCurrentPage(data)}>{data}</span>)
       )
   
       return (  
         <div id='pagination'>
             <div>
               총 글 갯수:{postListLength}
             </div>
             <div>
               페이지당 글 갯수:{postListPerPage}
             </div>
             <div>
               <span className='page' onClick={this.prevPage}>〈</span>
               {pageList}
               <span className='page' onClick={this.nextPage}>〉</span>
             </div>
         </div>
       );
     }
   }
   
   export default PagiNation;
   ```

   웹페이지 화면 ▼(1페이지에서 다음버튼 클릭)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166101138533632.png)

   ![image-20220821010338817](../../images/2022-08-19-class03(pagination)/image-20220821010338817.png)

   웹페이지 화면 ▼(2페이지에서 이전버튼 클릭)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166101157006434.png)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166101160467636.png)

   웹페이지 화면 ▼(첫번째 페이지에서 이동불가)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166101168857938.png)

   웹페이지 화면 ▼(마지막 페이지에서 이동불가)

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-166101182590340.png)

   <br><br>

4. 페이지네이션 하이라이트 적용

   이제 페이지네이션에 하이라이트를 적용하여 현재페이지 위치를 명확하게 나타냅니다.<br>

   먼저 첫페이지는 1페이지를 렌더링시키므로, 1페이지는 렌더링이 된 시점에서 하이라이트 적용이 되어있어야합니다.<br>

   `componentDidMound`함수는 DOM이 완성되고나서 자동으로 호출이 되므로 페이지네이션의 DOM 요소에 접근해 첫 번째 요소에만 하이라이트를 적용하면 됩니다. <br>

   원하는 페이지로 이동하기 위해서 특정 페이지네이션을 클릭하거나 이전, 다음 버튼을 눌러 이동할 때도 적용되도록하려면 아래의 코드와 같이 적용하면 됩니다. <br>

   ```react
   import '../css/PagiNation.css';
   import { Component } from 'react';
   
   class PagiNation extends Component {
   
     constructor(props){
       super(props)
       this.state={
         
       }
     }
   
     componentDidMount(){//DOM이 완성되고나서 자동호출
       var pageList=document.querySelectorAll('.page')
   
       pageList[1].style.color='darkgray'//css 속성에 접근 및 글자색 하이라이트 
       pageList[1].style.backgroundColor='black'//css속성에 접근 및 배경색 하이라이트
     }
   
   
     setPageHighLight=(page)=>{
       alert(page+"페이지 하이라이트!")
       //className="page"
       var pageList=document.getElementById('page'+page)//선택한 페이지만 하이라이트 적용하면 되므로 class대신 pageList에서 페이지네이션 생성시 추가로 id를 부여하고 해당 요소에 접근
       pageList.style.color="darkgray"
       pageList.style.backgroundColor="black"
     }
   
     setAllDefault=()=>{
       alert("모두해제!")
       var pageList=document.getElementsByClassName('page')//모든 페이지네이션 요소에 접근
       var pageListLength=pageList.length
       for(var i=0; i<pageListLength; i++){// 순차적으로 모두 default값으로 설정.. 
         pageList[i].style.color="black"
         pageList[i].style.backgroundColor="darkgray"
       } 
     }
   
   
   
   
     setCurrentPage=(page)=>{
       //alert("페이지번호 클릭됨!")
       alert(page+"페이지 클릭!")
       this.props.setCurrentPage(page)
       //App.js의 setCurrentPage함수
     }
   
     prevPage=()=>{
       const {currentPage,setCurrentPage} = this.props
       if(currentPage === 1){
         alert('이동불가!')
         return 
       }
       else{
         const prevPage = currentPage - 1 
         setCurrentPage(prevPage)        // 1. 페이지 설정, 2. 모든 페이지네이션 default처리 3. 선택된 페이지네이션(이전 버튼으로 선택된 현재 페이지 기준) 하이라이트 적용
         this.setAllDefault()
         this.setPageHighLight(prevPage)
       }
     }
   
     nextPage=()=>{
       const {currentPage,postListLength,postListPerPage,setCurrentPage} = this.props
       const endIndex = Math.ceil(postListLength/postListPerPage)
       if( currentPage === endIndex){
         alert('이동불가!')
         return 
       }
       else{
         const nextPage = currentPage + 1
         setCurrentPage(nextPage) // 1. 페이지 설정, 2. 모든 페이지네이션 default처리 3. 선택된 페이지네이션(다음 버튼으로 선택된 현재 페이지 기준) 하이라이트 적용
         this.setAllDefault()
         this.setPageHighLight(nextPage)
       }
     }
   
     render(){
   
       const {postListLength,postListPerPage}=this.props
       //10,3
       //3,3,3,1 - 1페이지~4페이지, 10/3 -> 3.33 -> 4
       let pageNumbers=[];//페이지 번호가 들어갈 배열
       console.log(postListLength)//10
       console.log(postListPerPage)//3
       const lastPageNum=Math.ceil(postListLength/postListPerPage)//4
       for(var i=1; i<=lastPageNum; i++){//1~4
         pageNumbers.push(i)//1,2,3,4
       }
       console.log(pageNumbers)//[1,2,3,4]
   
       const pageList=pageNumbers.map(
         (data)=>(<span className='page' key={data} id={'page'+data}
         onClick={()=>{this.setCurrentPage(data); this.setAllDefault(data); this.setPageHighLight(data) }}>{data}</span>)
       )
       //1. 페이지 설정, 2. 모든 페이지네이션 default값으로 설정, 3. 선택한 페이지네이션(해당 페이지네이션을 직접 클릭) 하이라이트 적용..
   
       return (  
         <div id='pagination'>
             <div>
               총 글 갯수:{postListLength}
             </div>
             <div>
               페이지당 글 갯수:{postListPerPage}
             </div>
             <div>
               <span className='page' onClick={this.prevPage}>〈</span>
               {pageList}
               <span className='page' onClick={this.nextPage}>〉</span>
             </div>
         </div>
       );
     }
   }
   
   export default PagiNation;
   ```

   웹페이지 화면 ▼

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-16615119064151.png)<br>

   다음페이지 클릭(2페이지 클릭) ▼

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-16615123281045.png)<br>

   다음페이지 전환 및 하이라이트 적용(2페이지) ▼

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-16615122640433.png)<br>

   이전페이지 클릭(1페이지 클릭) ▼

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-16615133994167.png)<br>

   이전페이지 전환 및 하이라이트 적용(1페이지)▼

   ![모두연동](../../images/2022-08-19-class03(pagination)/모두연동-16615134993559.png)<br><br><br><br>

   ref) https://bsscl.tistory.com/70 리액트 이벤트 즉시실행 문제