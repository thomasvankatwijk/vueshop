<template>
  <div class = "cart"><div class="cart-inner">
      <div @click="$emit('toggle-cart')" class = "cart-open">X</div>
    <h1 class="space">Cart</h1>
    <div class="inner-cart">
    <div v-for="item in cart" :key="item.id">
      <p>{{ item.title}}</p>
      <img :src="getImgUrl(item.img)"/>
 <button @click="$emit('delete-cart-item', item.id)">remove X</button>
    </div>
    </div>
  </div>
  </div>
</template>
<script>
export default {
  name: "Cart",
  props:{
      cart: Array,
  },
  

 methods:{
      getImgUrl: function (imagePath) {
      return require('@/assets/' + imagePath);
    },

   

  },
 emits: ['delete-cart-item', 'toggle-cart'],
  }

</script>