<template>
      <div class="todo-footer" v-show="this.todos.length">
        <label>
          <input type="checkbox" :checked="countall" @change="clickAll"/>
        </label>
        <span>
          <span>已完成{{count}}</span> / 全部{{todos.length}}
        </span>
        <button class="btn btn-danger" @click="clearDone">清除已完成任务</button>
      </div>
</template>

<script>
    export default {
        name: "TodoFooter",
        props:["todos", "clickAllApp", "clearDoneApp"],
        computed:{
            count(){
                return this.todos.filter((todo)=>{
                    return todo.isCheck === true
                }).length
            },
            countall(){
                return this.count === this.todos.length && this.count > 0
            }
        },
        methods:{
            clickAll(e){
                this.clickAllApp(e.target.checked)
            },
            clearDone(){
                this.clearDoneApp()
            }
        }
    }
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}



.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}
</style>