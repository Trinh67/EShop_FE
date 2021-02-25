<template>
  <div class="home">
    <ShopManager @reloadData="reload"/>
  </div>
</template>

<script>
// @ is an alias to /src
import ShopManager from '@/views/dictionary/shop/ShopList.vue';

export default {
  name: 'Home',
  components: {
    ShopManager
  },
  methods: {
    /**
     * Load lại dữ liệu
     * Created by: TXTrinh (23/02/2021)
     */
    reload(){
      this.$emit('reloadData')
    },
  },
}
</script>
