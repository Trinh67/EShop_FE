<template>
    <div class="navbar">
        <div class="logo-site">
            <div class="logo-box">
                <div class="amis-logo"></div>
            </div>
        </div>
        <div class="navbar-content">
            <a class="nav-item">
                <div class="nav-item-icon nav-item-dashboard"></div>
                <div class="nav-item-text">Tổng quan</div>
            </a>
            <a class="nav-item">
                <div class="nav-item-icon nav-item-report"></div>
                <div class="nav-item-text">Báo cáo</div>
            </a>
            <a class="nav-item">
                <div class="nav-item-icon nav-item-bill"></div>
                <div class="nav-item-text">Đơn hàng</div>
            </a>
            <a class="nav-item">
                <div class="nav-item-icon nav-item-buy"></div>
                <div class="nav-item-text">Mua hàng</div>
            </a>
            <router-link class="nav-item" to="/dictionary/sale">
                <div class="nav-item-icon nav-item-promotion"></div>
                <div class="nav-item-text">Khuyến mại</div>
            </router-link>
            <router-link class="nav-item" to="/dictionary/shop">
                <div class="nav-item-icon nav-item-manage"></div>
                <div class="nav-item-text">Quản lí cửa hàng</div>
            </router-link>
            <a class="nav-item">
                <div class="nav-item-icon nav-item-product"></div>
                <div class="nav-item-text">Hàng hóa</div>
            </a>
        </div>
    </div>
</template>
<script>
export default {
  name: 'MenuBarLinks',
  data () {
    return {
      Sale: '/dictionary/sale',
      Shop: '/dictionary/shop'
    };
  }
};
</script>
