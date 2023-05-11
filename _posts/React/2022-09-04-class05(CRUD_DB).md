---
categories: Coding	
tag: react
toc: true
---



# 2022. 08. 30. 수업내용 정리 #

## CRUD 구현 with nodeJS, mySQL 

<br>

* 도입

  지난번엔 `state`에 직접 `json array`로 데이터를 추가했지만, 이번엔 mySQL 내부에 있는 데이터를 이용해서 `CRUD`를 구현해보도록 하겠습니다.

  <br><br>

* Read

  직접 `state`에서 데이터를 만들었던 것과 다르게 이번에 서버(mySQL)에 있는 데이터를 받아온 후 화면에 렌더링 시키는 과정으로 진행하겠습니다. <br>

  `nodeJS` 강의 때처럼 서버구축은 `mySQL`과 연동해서 진행하고, 리액트에서는 `axios`를 이용해 서버에 요청을 보내줍니다. <br>

  서버에서 데이터를 불러오는 동안 렌더링도 동시에 진행될 수 있도록 비동기처리(async,await) 방식을 이용합니다. <br><br>

  **REACT**

  ```react
  // App.js 
  
  import './App.css';
  import { Component } from 'react';
  import axios from 'axios';
  import Person from './components/Person';
  import InputComp from './components/InputComp';
  class App extends Component {
  
    constructor(props){
      super(props)
      this.state={
        personList:[]//이번에는 빈 배열로 
      }
    }
  
    selectAll=async()=>{
      const result=await axios.get('./person')//비동기로 처리했으므로 서버의 응답 유무와 상관없이 다음 코드의 동작을 실행시킬 수 있음.. 
      console.log(result) //Object.. 여기서 result는 위의 get요청에 의해 받아온 sql서버의 DB(json 배열)입니다. 
      console.log(result.data) // json 배열 중  
      this.setState({
        personList:result.data
      })
    }
  
    render(){
  
      const result=this.state.personList.map(
        (data,index)=>(<Person key={data.name + index} name={data.name} 
          age={data.age} 
          height={data.height}/>)
      )
  
      return (
        <div id="app">
          <InputComp addPersonInfo={this.addPersonInfo}/>
          <button onClick={this.selectAll}>모두조회</button>
          {result}
        </div>
      );
    }
  }
  
  export default App;
  
  ```

  <br>

  SQL에서 받아온 DB, 위쪽이 `result`, 아래쪽이 `result.data` 를 콘솔에 출력한 것.

  ![image-20220905014125980](../../images/2022-09-04-class05(CRUD_DB)/image-20220905014125980.png)

  <br>

  ```react
  //person.js
  
  import '../css/Person.css'
  import { Component } from 'react';
  class Person extends Component{
  
      constructor(props){
          super(props)
          this.state={
           
          }
      }
  
  
      render(){
          return(
            <div id='person'>
                <div>이름:{this.props.name}</div>
                <div>나이:{this.props.age}</div>
                <div>키:{this.props.height}</div>
                <button>삭제</button>
                <button>수정</button>
            </div>
          )
      }
  
  }
  
  export default Person;
  ```

  ```react
  //InputComp.js
  
  import '../css/InputComp.css';
  import {Component} from 'react';
  class InputComp extends Component{
      constructor(props){
          super(props)
          this.state={
          }
      }
  
  
      render(){
          return(
              <div id='input-comp'>
                  <input type='text'/>
                  <input type='text'/>
                  <input type='text'/>
                  <button>추가</button>
              </div>
          )
      }
  }
  
  export default InputComp;
  ```

  <br><br>

  **Server Side**

  ```javascript
  //server.js
  
  const express = require('express');
  const app = express();
  const PORT = process.env.PORT || 4000;
  const db = require('./config/db.js')
  const bodyParser = require('body-parser')
  app.use(bodyParser.json())
  
  app.get('/hello',(req,res)=>{
      console.log('/hello')
  })
  
  app.get('/person',(req,res)=>{
      console.log('/person')
      db.query("select * from practice",(err,data)=>{ // mySQL practice database에서 practice table의 모든 데이터 조회
          if(!err){
              //console.log(data)
              res.send(data) //App.js로 보낸 DB
              console.log(data)
          }else{
              console.log(err)
          }
      })
  })
  
  
  app.listen(PORT, () => {
      console.log(`Server On : http://localhost:${PORT}/`);
  })
  ```

  ```javascript
  //db.js
  
  var mysql= require('mysql')
  const db=mysql.createPool({
      host:'localhost',// 로컬에서 동작
      user:'root',//sql 설치시 최초로 지정한 사용자명
      password:'*wish13241320',// 본인이 설정한 비밀번호
      database:'practice',// 사용할 sql 상에서의 데이터베이스
      port:3306 // sql default port
  })
  
  module.exports = db; //외부에서 호출할 수 있도록 함
  ```

  ```json
  //package.json
  
  {
    "name": "react-practice0",
    "version": "0.1.0",
    "private": true,
    "dependencies": {
      "@testing-library/jest-dom": "^5.16.5",
      "@testing-library/react": "^13.3.0",
      "@testing-library/user-event": "^13.5.0",
      "axios": "^0.27.2",
      "body-parser": "^1.20.0",
      "express": "^4.18.1",
      "mysql": "^2.18.1",
      "react": "^18.2.0",
      "react-dom": "^18.2.0",
      "react-scripts": "5.0.1",
      "web-vitals": "^2.1.4"
    },
    "proxy":"http://localhost:4000", //nodeJS 서버 PORT.. 3000번은 이미 REACT에서 사용중.. 
    "scripts": {
      "start": "react-scripts start",
      "build": "react-scripts build",
      "test": "react-scripts test",
      "eject": "react-scripts eject"
    },
    "eslintConfig": {
      "extends": [
        "react-app",
        "react-app/jest"
      ]
    },
    "browserslist": {
      "production": [
        ">0.2%",
        "not dead",
        "not op_mini all"
      ],
      "development": [
        "last 1 chrome version",
        "last 1 firefox version",
        "last 1 safari version"
      ]
    }
  }
  
  ```

  웹페이지 화면 ▼(Client)

  <br>(두 번째 데이터의 나이는 299 → 29로 수정했습니다.)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623111873522.png)

  Server(mySQL) ▼

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623114246186.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623113041534.png)

  <br><br>

* Create

  이번에는 생성입니다. <br>

  주목할 것은 `InputComp.js`에서 `inputChange(e)` 부분입니다.<br>

  리액트 이벤트 조작(`[e.target.name]:e.target.value`)을 통해서 입력한 값을 `state`에 넣어주는데 이벤트의 대상인 `input`에 접근 후 해당 `input`의 속성 중 `name`이라는 속성에 접근해 그 값을 `key`로 사용합니다. <br>

  이 때, 각 `name`속성의 값은 `state`에서 선언한 프로퍼티와 동일하므로 `state`값을 변경할 수 있게됩니다. <br>

  이전에는 `name`,`age`,`height` 각 부분에 대해서 개별적으로 함수를 만들어 진행했었지만, 이렇게 만들 경우 보다 간결하게 코드를 작성할 수 있습니다. <br>

  `App.js`에서 새롭게 추가할 데이터를 넣기 위해 `personObj`이라는 객체를 생성하고 `array.concat`을 통해 `personList`에 추가한 뒤 `personObj`은 서버로 전송해줍니다. <br>

  참고로 **`Create`** 부터는 전송할 데이터를 분류해야하므로 비동기(async, await)가 아닌 일반적인 형태로 작성해줍니다.<br>

  **REACT**

  ```react
  //App.js
  
  import './App.css';
  import { Component } from 'react';
  import axios from 'axios';
  import Person from './components/Person';
  import InputComp from './components/InputComp';
  class App extends Component {
  
    constructor(props){
      super(props)
      this.state={
        personList:[]
      }
    }
  
    selectAll=async()=>{
      const result=await axios.get('./person')
      console.log(result) 
      console.log(result.data)
      this.setState({
        personList:result.data
      })
    }
  
    addPersonInfo=(name,age,height)=>{
  
      const personObj={name:name,age:age,height:height}
      const concatPersonList=this.state.personList.concat(personObj)
      console.log(personObj) 
      this.setState({
        personList:concatPersonList
      })
  
      axios.post('./add/person1',personObj)
    }
  
  
    render(){
  
      const result=this.state.personList.map(
        (data,index)=>(<Person key={data.name + index} name={data.name} 
          age={data.age} 
          height={data.height}
          deletePerson={this.deletePerson}
          updatePerson={this.updatePerson}/>)
      )
  
      return (
        <div id="app">
          <InputComp addPersonInfo={this.addPersonInfo}/>
          <button onClick={this.selectAll}>모두조회</button>
          {result}
        </div>
      );
    }
  }
  
  export default App;
  ```

  ```javascript
  //InputComp.js
  
  
  import '../css/InputComp.css';
  import {Component} from 'react';
  class InputComp extends Component{
      constructor(props){
          super(props)
          this.state={
              name:'',
              age:'',
              height:''
          }
      }
  
      addPersonInfo=()=>{ 
          //~~~~화면추가~~~~
          const {name,age,height}=this.state
          this.props.addPersonInfo(name,age,height)//입력한 값으로 state로 변경한 후 함수를 통해 App.js로 parameter를 전달.  
          //axios.post('/add/person',personObj)
          //이 클라이언트의 요청을 받는 부분을 서버에 만들고
          // ~~~ app.post('/add/person',())
      }
  
      inputChange=(e)=>{
          this.setState({
              [e.target.name]:e.target.value// 객체 안에서 key를 [ ]로 감싸면 그 안에 넣은 레퍼런스가 가리키는 실제 값(이벤트의 대상인 input의 속성중 name 속성)이 key 값으로 사용됨.
          })                                // 각각의 name의 value는 순서대로 'name','age','height'을 가리키므로 
      }                                     // state에서 선언한 'name','age','height'과 매칭이 됩니다. 따라서 입력한 값으로 state값을 
  										  // 변경할 수 있게됩니다. 
      render(){
          return(
              <div id='input-comp'>
                  <input type='text' onChange={this.inputChange} name='name'/>
                  <input type='text' onChange={this.inputChange} name='age'/>
                  <input type='text' onChange={this.inputChange} name='height'/>
                  <button onClick={this.addPersonInfo}>추가</button>
              </div>
          )
      }
  }
  
  export default InputComp;
  ```

  <br>

  **Server Side**

  ```javascript
  // server.js
  
  const express = require('express');
  const app = express();
  const PORT = process.env.PORT || 4000;
  const db = require('./config/db.js')
  const bodyParser = require('body-parser')
  app.use(bodyParser.json()) // 클라이언트 측에서 JSON 형식의 바디({name:abc,age:12,height:155})를 보내면 서버측에서 req.body 혹은                                  // req.body.name, req.body.age... 등의 형식으로 자료를 읽을 수 있습니다.  
  
  app.get('/hello',(req,res)=>{
      console.log('/hello')
  })
  
  app.get('/person',(req,res)=>{
      console.log('/person')
      db.query("select * from practice",(err,data)=>{
          if(!err){
              //console.log(data)
              res.send(data)
              console.log(data)
          }else{
              console.log(err)
          }
      })
  })
  
  app.post('/add/person',(req,res)=>{ // 클라이언트에서 받아온 정보들을 서버에 추가 
      console.log('/add/practice1')
      console.log(req.body)
      const name=req.body.name 
      const age=req.body.age
      const height=req.body.height
      
      db.query(`insert into practice(name,age,height) values('${name}',${age},${height})`,(err,data)=>{
          if(!err){
              //console.log(data)
              console.log(data);
          }else{
              console.log(err)
          }
      })
  
  })
  
  
  app.listen(PORT, () => {
      console.log(`Server On : http://localhost:${PORT}/`);
  })
  ```

  <br>

  웹페이지 화면 ▼(Client)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623663185643.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623664704325.png)

  Server(mySQL)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166236847214619.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623665774967.png)

  <br><br>

* Delete

  삭제의 경우 `array.filter`를 이용해 제거할 데이터를 고른 후 Client에서는 해당 데이터를 제거한 뒤 재배열을 시키고 서버에는 제거한 데이터만 전송해야합니다. <br>

  이 때, 전송되는 데이터의 타입이 `JSON`이므로 `index[0]`를 통해 해당 객체에 접근한 후 속성에 접근해야합니다. <br>

  비동기(async, await)를 통해 서버로 데이터를 전송하는 것을 동시에 해버리면 `undefined` 가 전송되니 주의! 이는 **`Update`**에서도 동일합니다.<br>

  **REACT**

  ```react
  //App.js
  
  import './App.css';
  import { Component } from 'react';
  import axios from 'axios';
  import Person from './components/Person';
  import InputComp from './components/InputComp';
  class App extends Component {
  
    constructor(props){
      super(props)
      this.state={
        personList:[]
      }
    }
  
    selectAll=async()=>{
      const result=await axios.get('./person')
      console.log(result) //Object
      console.log(result.data)
      this.setState({
        personList:result.data
      })
    }
  
    addPersonInfo=(name,age,height)=>{
  
      const personObj={name:name,age:age,height:height}
      const concatPersonList=this.state.personList.concat(personObj)
      console.log(personObj) 
      this.setState({
        personList:concatPersonList
      })
  
      axios.post('./add/person1',personObj)
    }
  
    deletePerson=(name,age,height)=>{
      const filteredObj = this.state.personList.filter((data)=>((data.name !== name) && (data.age !== age) && (data.height !== height)))
      // 클라이언트에 삭제해야할 리스트를 제거하고 남은 데이터들을 재배열
      const deleteObj = this.state.personList.filter((data)=>(((data.name === name) && (data.age === age) && (data.height === height))))
      // 서버에 보낼 삭제할 리스트의 데이터를 추출 
      console.log(deleteObj)
      axios.post(`./delete/person2`,deleteObj)
      // 데이터를 수정.. (서버에 데이터를 전송해 수정하는 과정)
      this.setState({personList:filteredObj})
    }
  
  
    render(){
  
      const result=this.state.personList.map(
        (data,index)=>(<Person key={data.name + index} name={data.name} 
          age={data.age} 
          height={data.height}
          deletePerson={this.deletePerson}
          updatePerson={this.updatePerson}/>)
      )
  
      return (
        <div id="app">
          <InputComp addPersonInfo={this.addPersonInfo}/>
          <button onClick={this.selectAll}>모두조회</button>
          {result}
        </div>
      );
    }
  }
  
  export default App;
  ```

  ```react
  //Person.js
  
  import '../css/Person.css'
  import { Component } from 'react';
  class Person extends Component{
  
      constructor(props){
          super(props)
          this.state={
          }
      }
  
      deletePerson=()=>{
        alert("삭제!(Person.js)")
        alert("삭제할 이름:"+this.props.name)
        this.props.deletePerson(this.props.name,this.props.age,this.props.height)
          //App.js가 넘긴 삭제함수(선택한 영역에 있는 데이터의 속성들을 기준으로 함)
      }
      
  
      render(){
          return(
            <div id='person'>
                <div>이름:{this.props.name}</div>
                <div>나이:{this.props.age}</div>
                <div>키:{this.props.height}</div>
                <button onClick={this.deletePerson}>삭제</button>
                <button>수정</button>
            </div>
          )
      }
  
  }
  
  export default Person;
  ```

  <br>

  **Server Side**

  ```javascript
  //server.js
  
  const express = require('express');
  const app = express();
  const PORT = process.env.PORT || 4000;
  const db = require('./config/db.js')
  const bodyParser = require('body-parser')
  app.use(bodyParser.json())
  
  app.get('/hello',(req,res)=>{
      console.log('/hello')
  })
  
  app.get('/person',(req,res)=>{
      console.log('/person')
      db.query("select * from practice",(err,data)=>{
          if(!err){
              //console.log(data)
              res.send(data)
              console.log(data)
          }else{
              console.log(err)
          }
      })
  })
  
  app.post('/add/person1',(req,res)=>{
      console.log('/add/practice1')
      console.log(req.body) 
      const name=req.body.name
      const age=req.body.age
      const height=req.body.height
      
      db.query(`insert into practice(name,age,height) values('${name}',${age},${height})`,(err,data)=>{
          if(!err){
              //console.log(data)
              console.log(data);
          }else{
              console.log(err)
          }
      })
  
  })
  
  app.post('/delete/person2',(req,res)=>{
    const personObj = req.body[0] // JSON배열을 전달받았으므로 index로 객체에 직접 접근함.. 
    console.log(personObj)
    db.query(`delete from practice where name='${personObj.name}' and age=${personObj.age} and height=${personObj.height}`,(err,data)=>{
      if(!err){
          //console.log(data)
          console.log(data)
      }else{
          console.log(err)
      }
    })
  })
  
  app.listen(PORT, () => {
      console.log(`Server On : http://localhost:${PORT}/`);
  })
  ```

  웹페이지 화면 ▼(Client)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-16623672318579.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166236806404011.png)

  <br>

  Server(mySQL)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166236839318717.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166236811712713.png)

  

  <br><br>

* Update

  지난 번에 했었던 CRUD와 대부분 동일하지만, 서버로 전송해주기 위한 데이터(`updateItem`)를 분류하는 과정이 필요합니다. <br>

  또, 조건(선택한 `name`)에 따라 분류한 후 아직 해당 데이터의 `age`가 변경되지 않은 상태이므로 `Person.js`에서 받아온 `age`로 변경해주어야 합니다. <br>

  **REACT**

  ```react
  //App.js
  
  
  import './App.css';
  import { Component } from 'react';
  import axios from 'axios';
  import Person from './components/Person';
  import InputComp from './components/InputComp';
  class App extends Component {
  
    constructor(props){
      super(props)
      this.state={
        personList:[]
      }
    }
  
    selectAll=async()=>{
      const result=await axios.get('./person')
      console.log(result) //Object
      console.log(result.data)
      this.setState({
        personList:result.data
      })
    }
  
    addPersonInfo=(name,age,height)=>{
  
      const personObj={name:name,age:age,height:height}
      const concatPersonList=this.state.personList.concat(personObj)
      console.log(personObj) 
      this.setState({
        personList:concatPersonList
      })
  
      axios.post('./add/person1',personObj)
    }
  
    deletePerson=(name,age,height)=>{
      const filteredObj = this.state.personList.filter((data)=>((data.name !== name) && (data.age !== age) && (data.height !== height)))
      const deleteObj = this.state.personList.filter((data)=>(((data.name === name) && (data.age === age) && (data.height === height))))
      console.log(deleteObj)
      axios.post(`./delete/person2`,deleteObj)
      this.setState({personList:filteredObj})
    }
  
    updatePerson=(name,age)=>{// 이 때, age는 person.js에서 변경된 age..
      alert("수정!(App.js)")
      alert("수정대상 이름:"+name)
      alert("수정할 값:"+age)
  
      */
      // ...(삼점연산자-three dot opeartor) , map , =>
      // 재배열된 함수를 넣을 변수 생성 이후 다시 매핑.. 
      const updateStudentList=this.state.personList.map(
        (data)=>(data.name === name)? ({...data,age:age}):data 
          //person.js에서 수정버튼을 누른 리스트의 데이터'name'과 일치하는 데이터가 있을 경우에는 해당 데이터의 age항목을 바꾸고 'name'과  일           치하는 대상이 없을 경우 데이터 목록을 그대로 반환
      )//... spread operator (펼친다.)
      //data.name - state안에 있는 JSON배열의 원소의 name
      //name - 함수 매개변수가 받은 name
      const updateItem = this.state.personList.filter(//수정하는 항목의 조건에 해당하는 이름과 수정하는 사항인 나이를 전달
        (data)=>(data.name === name) // Person.js에서 전달받은 이름과 같은 데이터만 남기고 나머지는 모두 제외
      )
      updateItem[0].age = age // 새로 추출한 데이터에서 age(수정한 age)값 변경!
      console.log(updateItem)
      axios.put('./update/person3',updateItem)
      this.setState({
        personList:updateStudentList
      })
      
      
    }
  
    render(){
  
      const result=this.state.personList.map(
        (data,index)=>(<Person key={data.name + index} name={data.name} 
          age={data.age} 
          height={data.height}
          deletePerson={this.deletePerson}
          updatePerson={this.updatePerson}/>)
      )
  
      return (
        <div id="app">
          <InputComp addPersonInfo={this.addPersonInfo}/>
          <button onClick={this.selectAll}>모두조회</button>
          {result}
        </div>
      );
    }
  }
  
  export default App;
  ```

  ```react
  // Person.js
  
  
  import '../css/Person.css'
  import { Component } from 'react';
  class Person extends Component{
  
      constructor(props){
          super(props)
          this.state={
            edit:false,
            age:this.props.age //person 함수 내부에서 입력된 값을 받기 위해서 state에 선언
          }
      }
  
      deletePerson=()=>{
        alert("삭제!(Person.js)")
        alert("삭제할 이름:"+this.props.name)
        this.props.deletePerson(this.props.name,this.props.age,this.props.height)
          //App.js가 넘긴 삭제함수
      }
      
      updatePerson=()=>{
        alert("업데이트! Person.js")
        alert("업데이트! Person.js" + this.props.name)
        const {age,edit} = this.state
        const {name} = this.props
        if(edit === true) {
          this.props.updatePerson(name,age) // name은 조건용.. age는 수정할 값
        }
        this.setState({
          edit:!this.state.edit // 수정 버튼을 누를 때마다 토글(toggle).. 
        })
      }
  
      ageChange=(e)=>{
        console.log(e.target.value)
        this.setState({
          age:e.target.value 
        })
      }
  
      render(){
        const {edit} = this.state
        if(edit===false){ // 수정 불가능 모드.. 수정 버튼을 누르기 전
          return(
            <div id='person'>
                <div>이름:{this.props.name}</div>
                <div>나이:{this.props.age}</div>
                <div>키:{this.props.height}</div>
                <button onClick={this.deletePerson}>삭제</button>
                <button onClick={this.updatePerson}>수정</button>
            </div>
          )
        }
        else{
          return( // 수정 가능 모드.. 수정 버튼을 누른 후 
            <div id='person'>
                  <div>이름:{this.props.name}</div>
                  <div>나이:<input type="text" defaultValue={this.props.age} onChange={this.ageChange}/></div>
                  <div>키:{this.props.height}</div>
                  <button onClick={this.deletePerson}>삭제</button>
                  <button onClick={this.updatePerson}>수정</button>
            </div>
          )
        }
      }
  
  }
  
  export default Person;
  ```

  <br>

  **Server**

  ```javascript
  const express = require('express');
  const app = express();
  const PORT = process.env.PORT || 4000;
  const db = require('./config/db.js')
  const bodyParser = require('body-parser')
  app.use(bodyParser.json())
  
  app.get('/hello',(req,res)=>{
      console.log('/hello')
  })
  
  app.get('/person',(req,res)=>{
      console.log('/person')
      db.query("select * from practice",(err,data)=>{
          if(!err){
              //console.log(data)
              res.send(data)
              console.log(data)
          }else{
              console.log(err)
          }
      })
  })
  
  app.post('/add/person1',(req,res)=>{
      console.log('/add/practice1')
      console.log(req.body)
      const name=req.body.name
      const age=req.body.age
      const height=req.body.height
      
      db.query(`insert into practice(name,age,height) values('${name}',${age},${height})`,(err,data)=>{
          if(!err){
              //console.log(data)
              console.log(data);
          }else{
              console.log(err)
          }
      })
  
  })
  
  app.post('/delete/person2',(req,res)=>{
    const personObj = req.body[0]
    console.log(personObj)
    db.query(`delete from practice where name='${personObj.name}' and age=${personObj.age} and height=${personObj.height}`,(err,data)=>{
      if(!err){
          //console.log(data)
          console.log(data)
      }else{
          console.log(err)
      }
    })
  })
  
  app.put('/update/person3',(req,res)=>{
    const updateList = req.body[0]
    console.log(updateList)
    db.query(`update practice set age=${updateList.age} where name='${updateList.name}'`,(err,data)=>{
      if(!err){
          //console.log(data)
          console.log(data)
      }else{
          console.log(err)
      }
    })
  })
  
  app.listen(PORT, () => {
      console.log(`Server On : http://localhost:${PORT}/`);
  })
  ```

  웹페이지 화면 ▼(Client)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166237273864721.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166237282761223.png)

  <br>

  Server(mySQL)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166237290044625.png)

  ![crud](../../images/2022-09-04-class05(CRUD_DB)/crud-166237293523227.png)

  

  

  ref) <a href="https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%B2%98%EB%A6%AC-async-await">리액트비동기처리방식</a>

  ref) <a href="https://velog.io/@yejinh/express-%EB%AF%B8%EB%93%A4%EC%9B%A8%EC%96%B4-bodyParser-%EB%AA%A8%EB%93%88">body-parser</a>

  ref) <a href="https://smujihoon.tistory.com/205">리액트 이벤트 조작</a>

  ref) <a href="https://velog.io/@eunjin/OS-%EC%8B%B1%EA%B8%80%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98-%EC%9D%98%EB%AF%B8">싱글스레드_멀티스레드?</a>

  
