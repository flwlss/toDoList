<template>
  <div>
    <div v-for="(todo, i) in todos" :key="todo.id">
      <p>
        <span class="todo__id">{{ i + 1 }}. </span>
        <span
          class="todo__text"
          :class="{ todo__text_isShow: todo.isComplete }"
          @dblclick="removeItem(i)"
          >{{ todo.text }}</span
        >
        <input v-model="todo.isComplete" class="todo__check" type="checkbox" />
        <span>{{ isDone }}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: [Array],
      required: true,
    },
    removeTodo: {
      type: Function,
    },
  },
  methods: {
    removeItem(i) {
      this.$emit("removeTodo", i);
    },
  },
};
</script>