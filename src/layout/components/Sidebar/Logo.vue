<template>
  <div class="sidebar-logo-container" :class="{'collapse':collapse}">
    <transition name="sidebarLogoFade">
      <router-link key="collapse" class="sidebar-logo-link" to="/">
        <img src="@/assets/common/logo.png" class="sidebar-logo  ">
      </router-link>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'SidebarLogo',
  props: {
    collapse: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
    }
  }
}
</script>

<style lang="scss" scoped>
.collapse {
    .sidebar-logo {
      margin-left: 10px;
      width: 32px;
      height: 32px;
      // vertical-align: middle;
      vertical-align:text-top;
    }
  }
// 小图样式

.sidebar-logo {
      width: 140px;
      vertical-align: middle;
      margin-right: 12px;
      margin-left: 30px;
}
// 大图样式
</style>
