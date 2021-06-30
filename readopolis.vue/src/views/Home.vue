<template>
  <div class="home">
    <section class="hero is-small is-black mb-6">
        <div class="hero-body has-text-centered">
            <p class="title mb-6">
                Welcome to Readopolis
            </p>
            <p class="subtitle">
                The Best Online Book Store 
            </p>
        </div>
    </section>
    <div class="columns is-multiline">
      <div class="column is-12">
          <h2 class="is-size-2 has-text-black has-text-centered">Latest Books</h2>
      </div>

      <ProductBox 
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'


export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()
    document.title = 'Home | Readopolis'
  },
  methods: {
    async getLatestProducts(){
      
      this.$store.commit('setIsLoading', true)

      await axios
      .get('/api/v1/latest-products/')
      .then(response =>{
        this.latestProducts = response.data
      })
      .catch(error =>{
        console.log(error)
      })
      
      this.$store.commit('setIsLoading', false)

    }
  }
}
</script>
<style>
body {
background: rgb(163,247,247);
background: linear-gradient(90deg, rgba(163,247,247,1) 0%, rgba(167,248,248,1) 32%, rgba(255,253,134,1) 100%);
}
</style>