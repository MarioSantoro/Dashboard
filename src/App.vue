<script >
import SideBar from './components/SideBar.vue';
import Main from './components/Main.vue';
export default {
  data() {
    return {

    }
  },
  components: {
    SideBar,
    Main
  }
}
</script>

<template>
  <SideBar />
  <Main />
</template>

<style lang="scss">
@import url('../node_modules/bootstrap/scss/bootstrap.scss');
@import './general.scss'
</style>
