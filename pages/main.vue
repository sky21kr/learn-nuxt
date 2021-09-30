<template>
  <div>
    <h1>메인 페이지입니다.</h1>
    <div>
      <ul>
        <li v-for="product in products" :key="product.id">
          <img :src="product.imageUrl" :alt="product.name" />
          <p>{{ product.name }}</p>
          <p>{{ product.price }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData() {
    const response = await axios.get('http://localhost:3000/products')

    const products = response.data.map((item) => ({
      ...item,
      imageUrl: `${item.imageUrl}?random=${Math.random()}`,
    }))

    return { products }
  },

  // data() {
  //   return {
  //     products: [],
  //   }
  // },
  // async created() {},
}
</script>
