<script setup>
import { ref, onMounted } from 'vue'
import { fakeProducts } from '@/assets/data/product.js'

const count = ref(0)
const cart = ref([])

const loadCart = () => {
  const storage = localStorage.getItem('cart')
  // cart.value = storage ? JSON.parse(storage) : []
  // const cartIds = storage ? JSON.parse(storage) : []
  let cartIds = []
  if (storage) {
    try {
      cartIds = JSON.parse(storage)
    } catch (error) {
      localStorage.removeItem('cart')
    }
  }

  // 把資料中符合購物車id的篩選出來
  const result = fakeProducts.filter((item) => {
    return cartIds.includes(String(item.id))
  })
  // 把結果丟給cart
  cart.value = result
}

// 渲染到HTML的DOM tree
onMounted(() => {
  // debugger
  count.value = 1
  loadCart()
})
</script>

<template>
  <div class="cart">
    <h1>購物車</h1>
    <ul>
      <li v-for="item in cart" :key="item.id">
        <header>
          <img :src="item.image" :alt="item.name" />
          <div>
            <p>{{ item.name }}</p>
            <p>${{ item.price }}</p>
          </div>
        </header>
        <footer>
          <button>-</button>
          <span>1</span>
          <button>+</button>
        </footer>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
.cart {
  ul {
    list-style-type: none;
    li {
      margin-bottom: 0.5rem;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      border-bottom: 1px solid #ddd;
      padding: 0.5rem;
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
        gap: 1rem;
        button {
          width: 2.5rem;
          height: 2.5rem;
          border-radius: 50%;
        }
      }
    }
  }
}
</style>
