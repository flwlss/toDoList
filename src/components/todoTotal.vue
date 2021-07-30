<template>
  <div>
    <hr />
    <p>Список задач: {{ todos.length }}</p>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: [Object],
      required: true,
    },
  },
};
</script>