<template>
  <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
        <TodoHeader :addtodo="addtodo"></TodoHeader>
        <TodoList :todos="todos" :isCheckChangeApp="isCheckChangeApp" :deleteItemApp="deleteItemApp"></TodoList>
        <TodoFooter :todos="todos" :clickAllApp="clickAllApp" :clearDoneApp="clearDoneApp"></TodoFooter>
    </div>
  </div>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter.vue'
import TodoHeader from './components/TodoHeader.vue'
import TodoList from './components/TodoList.vue'

export default {
      name: 'App',
      components: {
        TodoFooter,TodoHeader,TodoList
      },
      data(){
          return{
              todos:[
                  {id:"001", title:"水浒传", isCheck:true},
                  {id:"002", title:"红楼梦", isCheck:false},
                  {id:"003", title:"三国演义", isCheck:false},
                  {id:"004", title:"西游记", isCheck:true},
              ]
          }
      },
    methods:{
          addtodo(obj){
              this.todos.unshift(obj)
          },
          isCheckChangeApp(id){
              this.todos.forEach( (todo) => {
                  if(todo.id === id){
                      todo.isCheck = !todo.isCheck
                  }
              })
          },
          deleteItemApp(id){
              this.todos = this.todos.filter( (todo) => {
                  return todo.id !== id
              })
          },
          clickAllApp(e){
                this.todos.forEach((todo) =>{
                    todo.isCheck = e
                })
          },
          clearDoneApp(){
              this.todos = this.todos.filter( (todo) => {
                  return !todo.isCheck
              })
          }

    }
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

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
