<template>
  <div class="container">
    <Title @deleteAll="deleteAll" @addTask="addTask"/>
    <List :startRange=startRange :currentPage=currentPage :totalPage=totalPage :tempTodos=tempTodos @deleteTask="deleteTask" @completeTask="completeTask" />
    <Button @prevBtn="prevBtn" @nextBtn="nextBtn" :currentPage=currentPage  @selectPage="selectPage" :totalPage=totalPage />
    
  </div>
</template>

<script>
import Button from './components/Button.vue'
import List from "./components/List.vue"
import Title from "./components/Title.vue"

export default {
  name: 'App',
  components: {
    Button , List, Title
  },
  data(){
    return {
      todos : [
        {
          content : "Test1",
          isDone : false
        },
        {
          content : "Test2",
          isDone : false ,

        },
        {
          content : "Test1",
          isDone : false
        },
        {
          content : "Test2",
          isDone : false ,
          
        },
        {
          content : "Test1",
          isDone : false
        },
        {
          content : "Test2",
          isDone : false ,
          
        }
      ],
      totalPage : 1,
      currentPage : 1,
      tempTodos : [],
      startRange : 0,
      endRange : 0
    }
  },
  mounted: function() {
    this.setPage();
    this.fetchData()
    console.log(this.currentPage)
  },
  methods: {
    addTask(value){
      this.todos.push({ content : value , isDone : false})
      this.fetchData()
      this.setPage()
    },
    deleteTask(index){
      this.todos.splice(index,1)
      if(this.currentPage != 1 && this.currentPage != 0 && this.tempTodos.length == 1){
        this.returnPage()
      }
      this.fetchData()
      this.setPage()
    },
    completeTask(index){
      console.log(index)
      if(this.todos[index].isDone){
        this.todos[index].isDone = false
      }else{
        this.todos[index].isDone = true
      }
    },
    selectPage(index){
      this.currentPage = index
      this.setPage
      this.fetchData()
            

    },
    prevBtn(){
      if(this.currentPage != 1){
        this.currentPage = this.currentPage - 1
      }
      this.fetchData()
    },
    nextBtn(){
      if(this.currentPage != this.totalPage){
        this.currentPage = this.currentPage + 1
      }
      this.fetchData()
    },
    returnPage(){
      this.currentPage = this.currentPage - 1
    },
    deleteAll(){
      this.todos = []
      this.totalPage = 1;
      this.currentPage = 1;
      this.fetchData()
    },
    setPage(){
      this.totalPage = Math.ceil(this.todos.length / 5 );
    },
    fetchData(){
      if(this.totalPage >= 1){
            this.startRange = (this.currentPage*5) -5;
            this.endRange =  this.currentPage*5
      }else{
            this.startRange = 0;
            this.endRange = this.todos.length - 1
        }
      this.tempTodos = this.todos.slice(this.startRange , this.endRange)
    }
  }
}
</script>

<style>
.headerbody, html {
  background: #093028; /* fallback for old browsers */
background: -webkit-linear-gradient(to left, #093028 , #237A57); /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to left, #093028 , #237A57); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
font-family: 'Roboto', sans-serif;
  cursor: default;
}
.container {
  width: 30%;
  margin : 30px auto;
}
.removeall {
  float: right;
  font-size: 0.4em;
  margin-right: 0%;
  line-height: 30px;
  padding-left: 1em;
  cursor: pointer;
}

.add {
  float:right;
  cursor: pointer;
}

#container {
  background: #7D3B44;
  width: 360px;
  margin: 100px auto;
  box-shadow: 0 0 3px rgba(0,0,0, 1);
}

h1 {
  background: #66202A;
  color: white;
  margin: 0;
  padding: 10px 20px;
  text-transform: uppercase;
  font-size: 24px;
  font-weight: normal;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.item {
  background: #66202A;
  max-height: 400px;
  line-height: 40px;
  color:  lightgray;
}

.item:nth-child(2n) {
  background: #7D3B44;
}
 

input {
  font-size: 15px;
  text-align: center;
  letter-spacing: 1px;
  background: #84593D;
  width: 100%;
  border: none;
  box-sizing: border-box;
  padding: 13px 13px 13px 20px;
  color: white;
  
}

input:focus {
  
  outline:none;
  border: 2px solid #84593D;
  color: white;
}
.completed {
  text-decoration: line-through;
  color: gray;
}

.item:hover {
  
  cursor: pointer;
}

span {
  background: #217353;
  height: 40px;
  margin-right: 20px;
  text-align: center;
  color: white;
  width: 0px;
  display: inline-block;
  transition: 0.2s linear;
  opacity: 0;
}

.item:hover span {
  width: 40px;
  opacity: 1;
}

::-webkit-input-placeholder { /* WebKit, Blink, Edge */
    color:    lightgray;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
   color:    lightgray;
   opacity:  1;
}
::-moz-placeholder { /* Mozilla Firefox 19+ */
   color:    lightgray;
   opacity:  1;
}
:-ms-input-placeholder { /* Internet Explorer 10-11 */
   color:    lightgray;
}
#pagin .current {
  background-color: yellow; 
}

#pagin li {
  width: 40px;
  height: 40px;
  line-height: 40px;
  display: inline-block;
  cursor: pointer;
  background: #7D3B44;
}
#pagin li a{
  margin-left: 14px;
}
.pagination1{
  background: #7D3B44;
}
.previousBtn{
  float: left;
  width: 70px !important;
  padding-left: 5px;
  color: green;
  padding-top: 8px;
  cursor: pointer;
  background: #7D3B44;
}
.nextBtn{
  padding-top: 8px;
  float: right;
  padding-right: 5px;
  color: green;
  cursor: pointer;
  background: #7D3B44;

}
.eplisis{
  width: 40px;
  height: 60px;
  text-align: center;
  pointer-events: none;
}
li{
    user-select: none; /* standard syntax */
    -webkit-user-select: none; /* webkit (safari, chrome) browsers */
    -moz-user-select: none; /* mozilla browsers */
    -khtml-user-select: none; /* webkit (konqueror) browsers */
    -ms-user-select: none; /* IE10+ */
}
</style>
