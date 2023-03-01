<template>
  <div className="avatar">
    <img :src="block.content">
  </div>
</template>

<script>
export default {
  name: "BlockAvatar",
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
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>