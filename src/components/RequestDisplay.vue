<template>
  <div class="container">
    <form class="form-inline" @submit.prevent="onSubmit">
      <div class="form-group mb-2">
        <label for="inputPassword2" class="sr-only">ID запроса</label>
        <input
          class="form-control"
          id="inputPassword2"
          placeholder="ID"
          v-model="id"
        />
      </div>
      <button type="submit" class="btn btn-primary mb-2 ml-2" @click="load">
        Сделать запрос!
      </button>
      <button
        type="submit"
        class="btn btn-danger mb-2 ml-2"
        @click="exampleLoad"
      >
        Очистить
      </button>
    </form>
    <div class="card card-body" v-if="gallery == null">{{ request }}</div>
    <div class="card card-body" v-else>{{ gallery }}</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      gallery: null,
      id: null,
      exampleMS: null,
    };
  },
  computed: {
    request() {
      let requests = "";
      if (this.gallery === "По вашему запросу ничего не найдено!") {
        requests = "По вашему запросу ничего не найдено!";
      } else {
        requests = this.exampleMS;
      }
      return requests;
    },
  },
  methods: {
    async load() {
      await axios
        .get(`https://boiling-refuge-66454.herokuapp.com/images/${this.id}`)
        .then(
          (response) => (this.gallery = response.data),
          (this.gallery = "По вашему запросу ничего не найдено!")
        )
        .catch(function (error) {
          alert("Ошибка! ", error);
          this.gallery = "По вашему запросу ничего не найдено!";
        });
    },
    async exampleLoad() {
      await axios
        .get("https://boiling-refuge-66454.herokuapp.com/images", {
          headers: {
            name: "value",
            test: "test",
          },
        })
        .then(
          (response) => (this.exampleMS = response.data),
          (this.gallery = null),
          (this.id = null)
        );
    },
  },
  mounted() {
    this.exampleLoad();
  },
  created() {
    let WP = "TestWP";
    const RP = "TestRP";
    /*
    {
      let test = { title: "Test", color: "red", margin: 1 };
      let { title, color, margin } = test;
      console.log(title);
      console.log(color);
      console.log(margin);
      let WP = "testWP Local";
      console.log(WP);
      console.log(RP);
    } */
    console.log(WP, " ", RP);

    /* Оператор спред
    const arr = [1, 2, 3, 4, 5];
    const data = [4, ...arr, 5];
    console.log(data); */

    /* Оператор рест
    const log = function (a, b, ...rest) {
      console.log(a, b, rest);
    };

    log("Basic", "rest", "operator", "usage"); */

    /* Параметры по умолчанию
    function multiply(a, b = 1) {
      return a * b;
    }

    multiply(5, 2);
    multiply(5);
    multiply(5, undefined);

    Для автоматической отправки куков withCredentials: true

    */
  },
};
</script>

<style lang="scss" scoped></style>
