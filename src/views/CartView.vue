<script setup>
import { fakeProducts } from '@/assets/data/product'
import { ref, onMounted } from 'vue'

const count = ref(0)
const cart = ref([])

const loadCart = () => {
  const storage = localStorage.getItem('cart')
  // cart.value = storage ? JSON.parse(storage) : []
  const cartIds = storage ? JSON.parse(storage) : []
  // 把資料中符合購物車id的篩選出來
  const result = fakeProducts.filter((item) => {
    return cartIds.includes(String(item.id))
  })
  // 把結果丟給cart
  cart.value = result
}

// 渲染到HTML的DOM tree
onMounted(() => {
  console.log('mount')
  //debugger
  count.value = 1
  loadCart()
})
</script>

<template>
  <div class="about">
    <h1>購物車</h1>
    <ul>
      <li v-for="item in cart" :key="item.id">
        <img :src="item.image" :alt="item.name" />
        <div>
          <p>{{ item.name }}</p>
          <p>{{ item.price }}</p>
          <p>
            <button></button>
          </p>
        </div>
      </li>
    </ul>
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
li {
  margin-bottom: 0.5rem;
  display: flex;
  flex-direction: row;
  justify-self: space-between;
}
header {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  img {
    height: 8rem;
    border-radius: 1rem;
  }
}
footer {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 0.5rem;
  button {
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
  }
}
</style>
