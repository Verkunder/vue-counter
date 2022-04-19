<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
};
</script>

<template>
  <div>
    <span
      class="badge m-2"
      :class="{
        'badge-warning': count == 0,
        'badge-primary': count > 0,
      }"
    >
      {{ count === 0 ? "Zero" : count }}
    </span>
    <button class="btn btn-secondary btn-sm" @click="count++">Increment</button>
  </div>
</template>

<style></style>
