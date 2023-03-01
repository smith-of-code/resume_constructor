<template>
  <p>
    {{block.content}}
  </p>
</template>

<script>
export default {
  name: "BlockP",
  props:{
    block:{
      type: Object,
      default:{
        content:''
      }
    }
  }
}
</script>

<style scoped>

</style>