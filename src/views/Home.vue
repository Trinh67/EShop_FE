<template>
  <div class="home">
    <ShopManager />
  </div>
</template>

<script>
// @ is an alias to /src
import ShopManager from '@/views/dictionary/shop/ShopList.vue';

export default {
  name: 'Home',
  components: {
    ShopManager
  }
}
</script>
