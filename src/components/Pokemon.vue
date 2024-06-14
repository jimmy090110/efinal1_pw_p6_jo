<template>
  <div class="container">
    <img :src="imagen" alt="" />
    <label for="">{{ texto }}</label>
  </div>
</template>

<script>
export default {
  props: {
    imagen: String,
    texto: String,
  },
};
</script>

<style>
.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
    
}
img {
  width: 250px;
  height: 250px;
  margin: 5px;
  margin-left: 10px;
  margin-right: 10px;
}
</style>