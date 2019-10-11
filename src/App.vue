<template>
  <div id="app">
    <addTodo v-on:add="pushTodo"/>
    <Todos v-bind:todos="todos" v-on:del="deleteTodo" v-on:update="updateTodo"/>
    <hr class="col-md-6 offset-md-3"/>
    <div class="col-md-6 mt-3 offset-md-3 d-flex justify-content-between">
      <div>Check all <input type="checkbox" :checked="checked" @change="checkAll"/></div>
      <div>Todos left: {{remaining}}</div>
    </div>
  </div>
</template>

<script>
import Todos from './components/Todos.vue'
import addTodo from './components/addTodo.vue'

export default {
  name: 'app',
  components:{
    Todos,
    addTodo,
  },
  computed:{
    remaining(){
      return this.todos.filter((todo) => todo.status !== true).length;
    },
    checked(){
      return this.remaining == 0;
    }
  },
  data(){
    return{
      todos:[
        {
          id:1,
          title:'Clean the house',
          status:true,
        },
        {
          id:2,
          title:'Read and Understand',
          status:false,
        },
        {
          id:3,
          title:'Watch the Flash S06',
          status:false,
        },
        {
          id:4,
          title:'Go to the Market',
          status:false,
        },
        {
          id:5,
          title:'Play football with Dami',
          status:true,
        },
      ]
    }
  },
  methods:{
    pushTodo(newTodo){
      this.todos.push(newTodo);
    },
    deleteTodo(todo){
       this.todos.splice(this.todos.indexOf(todo), 1);
    },
    checkAll(){
      // console.log('CheckAll');
      this.todos.forEach((todo) => todo.status = event.target.checked)
    },
    updateTodo(value){
      console.log(value);
      //  this.todos.splice(this.todos.indexOf(UpdatedTodo), 1, UpdatedTodo);
      
    }
  }
}
</script>

<style scoped>

</style>
