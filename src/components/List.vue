<template>
    <ul class="todoList" id="todoList">   
        <li v-bind:class="todo.isDone ? 'item completed' : 'item'" v-on:dblclick="completeTask(startRange + index)" v-for="(todo , index) in tempTodos" :key="index" >
                <span  v-on:click="deleteTask(startRange + index)">
                    <i class='fa fa-trash'   >  </i>
                </span>
                {{ todo.content}}
        </li>
        
	</ul>
</template>
<script>

export default {
  name: 'List',
  props: {
    todos : Array,
    startRange : Number,
    endRange : Number,
    tempTodos : Array,
    currentPage : Number,
    totalPage : Number
  },
  
  methods: {
      deleteTask(index){
        this.$emit("deleteTask" , index)
      },
      completeTask(index){
          this.$emit("completeTask" , index)
      },
      
  }
}
</script>
