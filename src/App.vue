<template>
 <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
     <Header @addTodo="addTodo"></Header>
     <List :todos="todos"></List>
     <Footer :todos="todos" :updateAll="updateAll" :deleteAll="deleteAll"></Footer>
    </div>
  </div>
</div>
</template>

<script>
import PubSub from 'pubsub-js'
import Header from '@/components/Header'
import List from '@/components/List'
import Footer from '@-todos/components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    List,
    Footer
  },
  mounted(){
    this.$bus.$on('deleteOne',this.deleteOne)
    PubSub.subscribe('heihei',this.updateOne)
  },
  data(){
    return{todos:JSON.parse(localStorage.getItem('TODOS_KEY'))||[]}
    
  },
  watch:{
    todos:{
      deep:true,
      handler(newVal,oldVal){
       localStorage.setItem('TODOS_KEY',JSON.stringify(newVal))
      }
    }
  },
methods:{
  addTodo(todo){
    this.todos.unshift(todo)
  },
  deleteComment(index){
   this.comments.splice(index,1)
  }
 
}
};
</script>

<style scoped>
/*app*/
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

</style>
