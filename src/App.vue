<template>
  <div id="app">
    <Header></Header>
    <Todo></Todo>
    <!-- <Footer></Footer> -->
  </div>
</template>

<script>
import Header from './components/header.vue'
import Footer from './components/footer.vue'
import Todo from './components/todo.vue'
export default {
  name: 'App',
  components:{
    Header,
    Footer,
    Todo
  }
}
</script>

<style lang="stylus" scoped>
#app 
  position absolute
  left 0
  right 0
  top 0 
  buttom 0
  #cover
    position absolute
    left 0
    right 0
    top 0
    buttom 0
    background-color #999
    opacity 0.5
    z-index -1

</style>
