<template>
  <div class="container">
    <div class="count">
      <div class="jumbotron jumbotron-fluid">
        <div class="container">
          <span :class="spanClass">
            {{ count === 0 ? "Zero" : count }}
          </span>
          <h1 class="display-4">{{ count === 0 ? "Zero" : count }}</h1>
        </div>
      </div>
      <div class="calculate">
        <button class="btn btn-dark" @click="count++">Добавить</button>
        <button class="btn btn-dark" @click="count--">Убавить</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["count"],
  computed: {
    spanClass() {
      let classes = "badge m-2 badge-";
      if (this.count == 0) {
        classes += "warning";
      }
      if (this.count > 0) {
        classes += "primary";
      }
      if (this.count < 0) {
        classes += "danger";
      }
      return classes;
    },
  },
  watch: {
    count(newCount) {
      console.log(newCount);
    },
  },
};
</script>

<style lang="css" scoped>
.count {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.jumbotron {
  max-width: 740px;
  width: 100%;
  text-align: center;
}
.btn-dark {
  margin: 0 5px;
}
.calculate {
  max-width: 750px;
  width: 100%;
  align-items: center;
  display: flex;
  justify-content: center;
}
</style>
