<template>
  <div>
    <p>{{ text }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    axios
      .get("https://swapi.dev/api/people/1")
      .then((response) => (this.text = response.data.name));
    return {
      text: String,
    };
  },
};
</script>

<style></style>
