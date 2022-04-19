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
  <div class="container">
    <button class="btn btn-secondary btn-sm" @click="alert">Click</button>
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
      <div class="form-group mb-2">
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
</template>

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
        .get("https://boiling-refuge-66454.herokuapp.com/images", {
          headers: {
            name: "value",
            test: "test",
          },
        })
        .then((response) => (this.exampleMS = response.data));
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

<style>
.container {
  padding: 15px 0;
}
.count {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.jumbotron {
  width: 740px;
  text-align: center;
}
.btn-dark {
  margin: 0 5px;
}
.calculate {
  width: 750px;
  align-items: center;
  display: flex;
  justify-content: center;
}
</style>
