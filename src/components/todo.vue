<template>
  <section class="todo-app">
    <input 
      type="text"
      class="add-input"
      autofocus="autofocus"
      placeholder="今天需要做......"
      @keyup.enter="addTodo"
    >
  
    <Item
      v-for="todo in filterTodos"
      :todo="todo"
      :key="todo.id"
      @del="deleteTodo"
    />
    <Tabs
      :filter="filter"
      :todos="todos"
      @toggle="toggleFilter"
      @clearAllTask="clearAllTask"
    />
  </section>
</template>

<script>
import Item from './item.vue';
import Tabs from './tabs.vue';
let id=0



export default {
    data() {
        return {
          todos:[],
          filter:'all'
        }
    },
    components:{
      Item,
      Tabs
    },
    computed: { 
      filterTodos(){
        if(this.filter === 'all'){
          return this.todos
        }
        const filterCompleted = this.filter === 'completed'
        return this.todos.filter(todo=>todo.completed === filterCompleted)
      }
     },
     methods:{
      addTodo(e){   
        if(e.target.value!=''){
          this.todos.unshift({
            id: id++,
            content:e.target.value,
            completed:false
          });
          e.target.value=''

        }
  
      },
      deleteTodo(id){
          this.todos.splice(this.todos.findIndex(todo => id===todo.id),1)
      },
      toggleFilter(state){
          this.filter =state
      },
      clearAllTask(){
          this.todos = this.todos.filter(todo =>{todo.completed === false || true})
      }
     }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  .todo-app
    width 600px
    margin 0 auto
    box-shadow 0 0 5px #666
  .add-input
    position relative
    margin 0
    width 100%
    font-size 24px
    font-family inherit
    font-weight inherit
    line-height 1.4em
    outline none
    color inherit
    padding 16px 16px 16px 36px
    box-sizing border-box
    border none
    box-shadow inset 0 -2px 1px rgba(0,0,0,0.033)
</style>
