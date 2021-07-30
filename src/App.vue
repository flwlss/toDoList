<template>
  <div id="nav">
    <h1 class="title">{{ title }}</h1>
    <div class="todo">
      <input v-model="todo" type="text" placeholder="type todo" />
      <button @click="addTodo(id++)">add todo</button>
      <p></p>
      <div v-for="(todo, i) in todos" :key="todo.id">
        <p>
          <span class="todo__id">{{ i + 1 }}.</span>
          <span
            class="todo__text"
            :class="{ todo__text_isShow: todo.isComplete }"
            @dblclick="removeToDo(i)"
            >{{ todo.text }}</span
          >
          <input
            v-model="todo.isComplete"
            class="todo__check"
            type="checkbox"
          />
          <span>{{ isDone }}</span>
        </p>
      </div>
      <hr />
      <p>Список задач: {{ todos.length }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      title: "toDoList",
      todo: " ",
      todos: [],
      id: 0,
    };
  },
  components: {},
  methods: {
    addTodo() {
      this.todos.push({
        id: this.id,
        text: this.todo,
        isComplete: false,
      });
      this.todo = " ";
    },
    removeToDo(i) {
      this.todos.splice(i, 1);
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
