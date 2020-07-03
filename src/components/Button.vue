<template>
  <div class="pagination1" >
    <div class="previousBtn" v-on:click="prevBtn">Previous</div>
    
    <div class="nextBtn" v-on:click="nextBtn" >Next</div>
                    <ul id="pagin" class="pagin1">
                        <li v-bind:class="currentPage == index ? 'pagili current' : 'pagili'" v-bind:id="index" v-on:click="selectPage(index)" v-for="index in totalPage" :key="index" >
                            <a href='#'>{{index}}</a> 
                      </li>
                    </ul>
    </div>
</template>

<script>

export default {
  name: 'Button',
  props: {
    totalPage : Number,
    currentPage : Number
  },
  
  methods: {
    selectPage(index){
      this.$emit('selectPage' , index)
    },
    prevBtn(){
      this.$emit('prevBtn')
    },
    nextBtn(){
      this.$emit('nextBtn')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
