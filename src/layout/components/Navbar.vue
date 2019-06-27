<template>
  <div class="vui-flex navbar pl15">
    <div>
      <hamburger :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />
    </div>
    <div class="vui-flex-item tr user">
      <img :src="avatar+'?imageView2/1/w/80/h/80'" class="user-avatar">
      <span class="t-grey f-s-12 mr10">admin</span>
      <el-button type="text" class="t-grey mr15" icon="el-icon-sold-out" @click="logout">注销</el-button>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Hamburger from '@/components/Hamburger'

export default {
  components: {
    Hamburger
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'avatar'
    ])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  line-height: 50px;
  overflow: hidden;
  position: relative;
  background: #fff;
  box-shadow: 0 1px 4px rgba(0,21,41,.08);
  .user{
    cursor: pointer;
  }
  .user-avatar {
    vertical-align: middle;
    width: 30px;
    height: 30px;
    border-radius: 50%;
  }
}
</style>
