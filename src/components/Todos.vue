<template>
    <div>
      <div v-for="todo in todos" v-bind:key="todo.id">
          <Todo v-bind:todo="todo" v-on:del="$emit('del',todo)" v-on:update="$emit('update',todo)"/>
      </div>
    </div>
</template>

<script>
import Todo from './Todo.vue'

export default {
    name:'Todos',
    components:{
        Todo
    },
    props:{
        todos:{
            required:true,
            type:Array,
        }
    }
}
</script>

<style>

</style>