<script>
import axios from "axios";
import $ from "jquery";
export default {
  data() {
    return {
      count: 0,
      gallery: null,
      id: null,
      exampleMS: null,
    };
  },
  methods: {
    alert() {
      if (confirm("Оставить комментарий?")) {
        alert("Комментарий отправлен");
      } else {
        alert("Комментарий не оставлен");
      }
    },
    postAxios() {
      axios
        .post(
          "https://boiling-refuge-66454.herokuapp.com/images/237/comments",
          {
            name: "Test",
            comment: "Test",
          }
        )
        .then(function () {
          alert("Успех!");
        })
        .catch(function (error) {
          alert("Ошибка! ", error);
        });
    },
    async postFetch() {
      const url =
        "https://boiling-refuge-66454.herokuapp.com/images/237/comments";
      const data = { name: "Test", comment: "test" };

      try {
        const response = await fetch(url, {
          method: "POST",
          body: JSON.stringify(data),
          headers: {
            "Content-Type": "application/json",
          },
        });
        const json = await response.json();
        alert("Успех:", JSON.stringify(json));
      } catch (error) {
        alert("Успех!", error);
      }
    },
    postJquery() {
      var request = $.ajax({
        url: "https://boiling-refuge-66454.herokuapp.com/images/237/comments",
        type: "POST",
        data: { name: "Test", comment: "test" },
        dataType: "html",
      });

      request.done(function () {
        alert("Done");
      });

      request.fail(function (textStatus) {
        alert("Request failed: " + textStatus);
      });
    },
    async load() {
      await axios
        .get(`https://boiling-refuge-66454.herokuapp.com/images/${this.id}`)
        .then((response) => (this.gallery = response.data));
    },
    async exampleLoad() {
      await axios
        .get("https://boiling-refuge-66454.herokuapp.com/images")
        .then((response) => (this.exampleMS = response.data));
    },
  },
  mounted() {
    this.exampleLoad();
  },
};
</script>

<template>
  <div class="container">
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
    <div class="container">
      <div class="row">
        <button class="btn btn-secondary btn-sm" @click="alert">Click</button>
      </div>
    </div>
    <div class="container">
      <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-primary" @click="postFetch">
          fetch
        </button>
        <button type="button" class="btn btn-success" @click="postAxios">
          Axios
        </button>
        <button type="button" class="btn btn-danger" @click="postJquery">
          jqueryAjax
        </button>
      </div>
    </div>
    <div class="container">
      <form class="form-inline" @submit.prevent="onSubmit">
        <div class="form-group mx-sm-3 mb-2">
          <label for="inputPassword2" class="sr-only">ID запроса</label>
          <input
            class="form-control"
            id="inputPassword2"
            placeholder="ID"
            v-model="id"
          />
        </div>
        <button type="submit" class="btn btn-primary mb-2" @click="load">
          Сделать запрос!
        </button>
      </form>
      <div class="card card-body" v-if="gallery == null">{{ exampleMS }}</div>
      <div class="card card-body" v-else>{{ gallery }}</div>
    </div>
  </div>
</template>

<style>
.container {
  padding: 15px 0;
}
</style>
