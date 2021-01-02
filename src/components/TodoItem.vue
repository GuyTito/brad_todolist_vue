<template>
  <div class="todo-item">
    <p :class="{'is-complete': todo.completed}">
          <input type="checkbox" @change="markComplete">
          {{todo.title}}
          <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods:{
        markComplete(){
            this.todo.completed = !this.todo.completed
        }
    }
}
</script>

<style scoped>
    .todo-item{
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }
    .is-complete {
        text-decoration: line-through;
    }
    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
    /* @media (prefers-color-scheme: dark) {
        .todo-item {
            color: #eee;
            background: #121212;
        }
    } */
</style>