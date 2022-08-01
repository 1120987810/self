<template>
    <div class="helper" >
        <span class="left">{{this.unfinishedTodo.length}} items left</span>
        <span class="tabs">
            <span v-for="state in states" :key="state" :class="[state, filter === state ?'actived':'']" @click="toggleFilter(state)">
             {{state}}
            </span>
       </span>
        <span class="clear" @click="clearAll">Clear</span>
    </div >
</template>

<script>
export default{
    props:{
        filter:{
            type: String,
            required:true
        },
        todos:{
            type: Array,
            required: true

        }
        
    },
    data(){
            return{
                states:['all', 'active', 'completed']
            }
        },
    computed:{
            unfinishedTodo(){
                return this.todos.filter(todo=> todo.completed === false)
            }
        },
    methods: {
            clearAll(){
                this.$emit('clearAllTask')
            },
            toggleFilter(state){
                this.$emit('toggle',state)
            }
        },
}
</script>
<style lang="stylus" scoped>
.helper
    font-weight 100
    display flex
    justify-content space-between
    padding 5px 0
    line-height 30px
    background-color #ffffff
    font-size 14px
    font-smoothing antialiased
.left,.clear,.tabs
    padding 0 10px
.left,.clear
    width 150px
.left   
    text-align left
.clear
    text-align center
    cursor pointer
.tabs
    width 200px
    display flex
    justify-content space-between
    *
        display inline-block
        padding 0 10px
        cursor pointer
        border-radius 10px
        &:hover
            background-color rgba(82 139 139,0.1)
        &.actived
            border-radius 10px
            background-color rgba(82 139 139,0.4)

</style>