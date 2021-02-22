<template>
  <div class="content">
    <router-view @reloadData="reload"/>
  </div>
</template>
<script>
export default {
  name: "Content",
  methods: {
    reload(){
      this.$emit('reload')
    }
  },
}
</script>