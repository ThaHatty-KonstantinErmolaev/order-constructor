<template>
  <input v-bind:type="input.type">
</template>

<script>
export default {
  name: "FormInput",
  props: {
    input: {
      type: Object
    },
  },
}
</script>

<style scoped>

</style>