<template>
  <h2>{{block.content}}</h2>
</template>

<script>
export default {
  name: "BlockH2",
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