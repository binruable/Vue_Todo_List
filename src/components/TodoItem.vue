<template>
        <li>
          <label>
            <input type="checkbox" :checked="todo.isCheck" @change="isCheckChange(todo.id)"/>
            <span v-show="!todo.isEdit">{{todo.title}}</span>
            <input :value="todo.title" v-show="todo.isEdit" @blur="handleEdit(todo, $event)" ref="jiaodian">
          </label>
          <button class="btn btn-danger" @click="deleteItem(todo.id)">删除</button>
          <button class="btn btn-edit" @click="editItem(todo)">编辑</button>

        </li>
</template>

<script>
    export default {
        name: "TodoItem",
        props:["todo","isCheckChangeApp", "deleteItemApp","editItemApp"],
        methods:{
            isCheckChange(id){
                this.isCheckChangeApp(id)
            },
            deleteItem(id){
                if(confirm("删除吗？")){
                    this.deleteItemApp(id)
                }
            },
          editItem(todo){
              todo.isEdit = true
            // 等节点更新完成之后再执行
              this.$nextTick(()=>{
                  this.$refs.jiaodian.focus()
              })
          },
          handleEdit(todo,e){
              this.editItemApp(todo.id, e.target.value)
              todo.isEdit = false
          }

        }
    }
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover{
    background-color: #cccccc;
}

li:hover button{
    display: block;
}
</style>