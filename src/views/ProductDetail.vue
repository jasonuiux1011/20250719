<script setup>
import { computed } from 'vue'
import { fakeProducts } from '@/assets/data/product'
const props = defineProps(['id'])

const product = computed(() => {
  return fakeProducts.find((item) => item.id === Number(props.id))
})

const addCart = () => {
  // 1.確認購物車裡面有沒有東西
  const addCart = localStorage.getItem('cart')
  // 2.如果有，解析他，沒東西放空陣列
  //   const cart = addCart ? JSON.parse(addCart) : []
  // 3.把商品加入購物車
  cart.push(props.id)
  localStorage.setItem('cart', JSON.stringify(cart))
  //   alert(`已加入購物車:商品${props.id}`)
  // console.log(newcart)
  let newcart = []
  if (oldCart && Array.isArray(oldCart)) {
    newcart = JSON.parse(oldCart)
  } else {
    newcart = []
    localStorage.removeItem('cart')
  }
}
</script>

<template>
  <div class="about">
    <h1>商品詳情</h1>
    <div>{{ product.name }}</div>
    <div>商品 ID：{{ props.id }}</div>
  </div>
  <button @click="addCart">加入購物車</button>
</template>
