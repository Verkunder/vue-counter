<template>
  <div class="container">
    <button class="btn btn-secondary btn-sm" @click="alert">Click</button>
  </div>
</template>

<script>
export default {
  methods: {
    alert() {
      if (confirm("Оставить комментарий?")) {
        alert("Комментарий отправлен");
      } else {
        alert("Комментарий не оставлен");
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
