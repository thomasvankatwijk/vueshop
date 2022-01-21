<template>

 <div class="products">
    <div class="product" :key="product.id" v-for="product in products"> 
 <div class="inner-product">
     <div class="product-title">{{product.title}}</div>
     <div class="img-box">
         <div>
      <img :src="getImgUrl(product.img)"/>
      </div>
      </div>
        <div class = 'product-txt'>
{{product.text}}

        </div>
        <button @click="$emit('add-to-cart', product)" class="btn btn-sm btn-primary">Add to Cart</button>
    </div>

    <!--
    <button @click="removeFromCart(product.id)" v-if="isInCart(product.id)">
        remove from cart
      </button>
       -->
      
     
      
       
  </div>
  </div>
</template>

<script>
export default {
  name: 'Products',
  props:{
      products: Array,
  }, 
  methods:{
      getImgUrl: function (imagePath) {
      return require('@/assets/' + imagePath);
    },

   

  },

  emits: ['add-to-cart'],

}

</script>