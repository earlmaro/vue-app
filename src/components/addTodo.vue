<template>
  <div>
      <div class="mt-4 container text-center col-md-6 ">
          <h3>What Needs to be done?</h3>
          <form class="d-flex" @submit.prevent="addTodo">
            <input type="text" placeholder="What the hell do you wanna do?" class="form-control" v-model="title" />
            <input type="submit" class="btn btn-primary" />
          </form>
      </div>
  </div>
</template>

<script>
export default {
    name:'addTodo',
    data(){
        return{
            title:''
        }
    },
    methods:{
        addTodo(){
            if(this.title.trim().length == 0){
                return
            };
            const newTodo = {
                id:10,
                title:this.title,
                status:false,
            };
            this.$emit('add',newTodo);

            this.title = '';
        }
    }
}
</script>

<style>

</style>