<template>
  <div class="product-box">
    <h1>{{ product.title }}</h1>
    <img :src="require(`../assets/images/${product.image}`)">
  </div>
</template>

<script>
export default {
  name: "ProductBox",
  props: ['product']
}
</script>

<style scoped>
  .product-box{
    padding: 10px;
    box-shadow: 0px 0px 6px black;
    width: 400px;
    height: 410px;
    margin: 10px;
    overflow: hidden;
    border-radius: 10px;
    border: none;
    background: #f7f7f7;
  }

  .product-box:hover{
    transform: scale(1.1, 1.1);
    cursor: pointer;
  }

  img {
    max-width: 80%;
    max-height: 80%;
  }
</style>