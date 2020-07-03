<template>
    <div>
        <h1>To-Do List<i class="removeall" v-on:click="deleteAll" >Clear</i><i class="add" >+</i></h1>
        <input type="text" v-model="newTask" @keyup.enter="addTask" id="name"  placeholder="[Add New Todo]"/>
    </div>
</template>
<script>
    export default {
        name: 'Title',
        props: {
        },
        data() {
            return {
            newTask: ''
            }
        },
        methods: {
            addTask(){
            if(this.newTask != ""){
                this.$emit('addTask' , this.newTask)
                this.newTask = ""
            }
            
        },
            
            deleteAll(){
                this.$emit("deleteAll")
            }
  }
}
</script>
