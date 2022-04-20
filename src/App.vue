<template>
  <Counter :count="count" />
  <Alert />
  <Requests />
  <RequestDisplay />
</template>

<script>
import Counter from "./components/Counter.vue";
import Alert from "./components/Alert.vue";
import Requests from "./components/Requests.vue";
import RequestDisplay from "./components/RequestDisplay.vue";
export default {
  data() {
    return {
      count: 0,
    };
  },
  components: {
    Counter,
    Alert,
    Requests,
    RequestDisplay,
  },
};
</script>

<style>
.container {
  padding: 15px 0;
}
</style>
