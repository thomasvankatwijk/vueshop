<template>
  <div id="app">
   <Header 
   title = "Shop"
   @toggle-cart = "toggleCart"
   />

<div v-if="showtheCart">
  <Cart 
  @delete-cart-item = "deleteCartItem"
  @toggle-cart = "toggleCart"
  :cart = "cart"/>
</div>
  <Products @add-to-cart = "addToCart"
  
  :products = "products"/>
  <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Cart from './components/Cart.vue'
import Products from './components/Products.vue'
import Footer from './components/Footer.vue'


export default {
  name: 'App',
  components: {
    Header,
    Cart,
    Products,
    Footer,
  },

      data(){
        return{
            products: [],
           cart: [],
           showtheCart: false
        }
    },
   
  

  methods:{
   
   toggleCart(){
this.showtheCart = !this.showtheCart
   },
    
     async addToCart(product) {
       if (!this.cart.find(({ id }) => id === product.id)){
      const res = await fetch('api/cart', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(product),
      })
      const data = await res.json()
      this.cart = [...this.cart, data]
      this.showtheCart = true
       }
       else{
         alert("Product is already in cart.")
       }
    },
      
  async fetchProducts() {
      const res = await fetch('api/products')
      const data = await res.json()
      return data
      //console.log(data)
      //console.log('test')
    },
      async fetchCart() {
      const res = await fetch('api/cart')
      const data = await res.json()
      return data
      //console.log(data)
      //console.log('test')
    },
    async deleteCartItem(id) {
      
        const res = await fetch(`api/cart/${id}`, {
          method: 'DELETE',
        })
        res.status === 200
          ? (this.cart= this.cart.filter((item) => item.id !== id))
          : alert('Error deleting item')
   
    },
  },
    
  
  async created() {
    this.products = await this.fetchProducts()
    this.cart = await this.fetchCart()
    
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
