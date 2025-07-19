<script setup>
import { computed } from 'vue'
import { fakeProducts } from '@/assets/data/product.js'
const props = defineProps(['id'])
const info = computed(() => {
  return fakeProducts.find((item) => {
    // console.log(item.id)
    // return item.id == props.id
    return item.id === Number(props.id)
  })
})

const addCart = () => {
  // 1. 確認購物車裡面有沒有東西
  const oldCart = localStorage.getItem('cart')

  // 2. 有東西解析他｜沒有東西給一個空陣列
  // const newCart = oldCart ? JSON.parse(oldCart) : []
  let newCart = []
  if (oldCart) {
    try {
      newCart = JSON.parse(oldCart)
    } catch (error) {
      localStorage.removeItem('cart')
    }
  }

  // 3. 把商品ID加入購物車
  newCart.push(props.id)
  localStorage.setItem('cart', JSON.stringify(newCart))
}
</script>

<template>
  <div class="about">
    <h1>商品詳情</h1>
    <!-- 找到路徑ID -->
    <div>{{ $route.params.id }}</div>
    <div>{{ props.id }}</div>
    {{ info }}
    <button @click="addCart">加入購物車</button>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
