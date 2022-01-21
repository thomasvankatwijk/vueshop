<template>
  <header>
      <div class="header-inner">
    <h1 class="big-title">{{ title }}</h1>
    <div @click="$emit('toggle-cart')" class = "cart-open">Cart &#x2192;</div>
  </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String,
   
  },

emits: ['toggle-cart'],

}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>