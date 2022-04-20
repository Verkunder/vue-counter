<template>
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
</template>

<script>
import axios from "axios";
import $ from "jquery";
export default {
  methods: {
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
  },
};
</script>

<style lang="scss" scoped></style>
