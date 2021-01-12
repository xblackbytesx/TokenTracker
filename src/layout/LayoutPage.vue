<template>
  <div class="app-shell">
    <div class="app-shell__page">
      <transition name="fade" mode="out-in">
        <keep-alive include="dashboard">
          <router-view />
        </keep-alive>
      </transition>
    </div>
    <header class="app-shell__header">
      <button
        class="back-btn"
        v-if="currentPage === 'infoview'"
        @click="$router.push({ path: '/' })"
      >
        <i class="fa fa-angle-left fa-2x"></i>
      </button>
      <span class="page-title">Token Tracker</span>
    </header>
  </div>
</template>
<script>
export default {
  name: "LayoutPage",
  data() {
    return {
      currentPage: "dashboard"
    };
  },
  watch: {
    $route: {
      deep: true,
      handler: function(page) {
        this.currentPage = page.name;
      }
    }
  }
};
</script>
<style>
.app-shell {
  display: flex;
  flex-flow: row wrap;

  &__header {
    text-align: center;
    width: 100%;
    height: 6vh;
    line-height: 50px;
    box-shadow: 0 6px 7px 0 rgba(68, 67, 67, 0.16);
    border-bottom: 2px solid var(--border-z1);
    background: var(--bgcolor-z1);
    transition: left 0.3s ease;
    order: 0;
    z-index: 5;
  }

  &__page {
    width: 100%;
    height: 94vh;
    overflow: auto;
    order: 2;
  }
}

.app-shell__header {
  .back-btn {
    position: absolute;
    background-color: transparent;
    left: 0;
    padding: 0 20px;
    margin: -1px 0;
    border: none;
    cursor: pointer;
    i {
      vertical-align: middle;
    }
  }
  .page-title {
    font-size: 25px;
    font-weight: bold;
  }
}
</style>
