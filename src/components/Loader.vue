<template>
  <div class="loader"></div>
</template>

<script>
export default {
  name: "Loader"
}
</script>

<style scoped>
.loader:before{
  background-color: #2c3e50;
}
.loader:after{
  background-color: #ffffff;
}
</style>