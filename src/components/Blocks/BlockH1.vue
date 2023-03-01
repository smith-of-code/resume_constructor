<template>
  <h1>{{block.content}}</h1>
</template>

<script>
export default {
  name: "BlockH1",
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