<template>
  <div id="app">
      <Navbar />
      <Header />
      <Content v-if="isPanel" @reload="reloadData"/>
  </div>
</template>

<script>
import Navbar from "@/components/layout/Navbar";
import Header from "@/components/layout/Header";
import Content from "@/components/layout/Content";

export default {
  name: "App",

  components: {
    Navbar,
    Header,
    Content,
  },

  data: () => ({
    //
    isPanel: true,
  }),
  methods:{
    reloadData() {
      this.isPanel = false;
      this.$nextTick(() => {
        this.isPanel = true;
      });
    }
  },
}
</script>

<style lang='scss'>
@import "./styles/index.scss";

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50 !important;
}

#nav a.router-link-exact-active {
  color: #019160;
}
.navbar .navbar-content .nav-item.router-link-exact-active {
  background-color: #00577b;
}
</style>
