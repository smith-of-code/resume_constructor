<template>
  <h3>{{block.content}}</h3>
</template>

<script>
export default {
  name: "BlockH3",
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