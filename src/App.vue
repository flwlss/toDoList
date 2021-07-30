<template>
  <div id="nav">
    <h1 class="title">{{ title }}</h1>
    <div class="todo">
      <input v-model="todo" type="text" placeholder="Задание" />
      <button @click="addTodo(id++)">Добавить</button>
      <p></p>
      <todo-list :todos='todos' @removeTodo='removeTodo'/>
      <todo-total :todos='todos'/>
    </div>
  </div>
</template>

<script>
import todoList from '@/components/todoList.vue'
import todoTotal from '@/components/todoTotal.vue'

export default {
  name: "Home",
  data() {
    return {
      title: "toDoList",
      todo: "",
      todos: [],
      id: 0,
    };
  },
  mounted() {
    const data = localStorage.getItem("todos");
    if (data) {
      this.todos = JSON.parse(data);
    }
  },
  components: {
    todoList,
    todoTotal
  },
  methods: {
    addTodo() {
      if (this.todo != "") {
        this.todos.push({
          id: this.id,
          text: this.todo,
          isComplete: false,
        });
        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
      this.todo = "";
    },
    removeTodo(i) {
      this.todos.splice(i, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style lang="scss">
.title {
  text-align: center;
}
.todo {
  width: 300px;
  height: 100%;
  background: #fff2f2;
  padding: 30px;
  outline: 1px solid #000;
  min-height: 500px;

  &__id {
    color: red;
    font-weight: bold;
  }

  &__text {
    font-size: 15px;
    color: #444;
    text-transform: capitalize;

    &_isShow {
      color: #ccc;
      text-decoration: line-through;
    }
  }

  &__check {
    display: inline-block;
    margin-left: 10px;
  }
}
</style>
