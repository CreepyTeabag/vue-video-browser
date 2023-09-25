<template>
  <div>
    <!-- v-on:input="onInput" = @input -->
    <input @input="onInput" />
  </div>
</template>

<script>
// this is basically te same as writing inside of 'new Vue'
export default {
  name: "SearchBar",
  methods: {
    onInput: function (event) {
      this.$emit("termChange", event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 75%;
}
div {
  text-align: center;
  margin: 20px;
}
</style>
