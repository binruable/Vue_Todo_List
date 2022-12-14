<template>
  <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
        <TodoHeader :addtodo="addtodo"></TodoHeader>
        <TodoList :todos="todos"
                  :isCheckChangeApp="isCheckChangeApp"
                  :deleteItemApp="deleteItemApp"
                  :editItemApp="editItemApp"
        >

        </TodoList>
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
              todos:JSON.parse(localStorage.getItem("todos"))
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
          },
          editItemApp(id, value){
            this.todos.forEach((todo) => {
              if(todo.id === id){
                if(value.trim() === ""){
                  alert("不能为空")
                  return
                }
                todo.title = value
              }
            })
          }

    },
    watch:{
        todos:{
          deep:true,
          handler(value){
             localStorage.setItem("todos",JSON.stringify(value))
          }
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
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-edit {
  color: #fff;
  background-color: skyblue;
  border: 1px solid skyblue;
  margin-right: 10px;
}

</style>
