<script setup>
import { fakeProducts } from '@/assets/data/product.js'
console.log(fakeProducts)
</script>

<template>
  <div class="product">
    <h1>商品列表</h1>
    <ul>
      <li v-for="item in fakeProducts" :key="item.id">
        <RouterLink :to="`/product/${item.id}`">
          <img :src="item.image" :alt="item.name" />
          <h1>{{ item.name }}</h1>
        </RouterLink>
        <p>{{ item.price }}</p>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
.product {
  ul {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    li {
    }
  }
  img {
    width: 100%;
    height: auto;
  }
}
</style>
