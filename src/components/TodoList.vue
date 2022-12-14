<template>
  <ul class="todo-main">
        <todo-item
                v-for="todo in todos"
                :key="todo.id"
                :todo="todo"
                :isCheckChangeApp="isCheckChangeApp"
                :deleteItemApp="deleteItemApp"
                :editItemApp="editItemApp">

        </todo-item>
  </ul>

</template>

<script>
    import TodoItem from "@/components/TodoItem";
    export default {
        name: "TodoList",
        components: {TodoItem},
        props:["todos","isCheckChangeApp","deleteItemApp","editItemApp"]
    }
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>