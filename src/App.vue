<template>
  <the-header></the-header>
  <router-view v-slot="slotProps">
  <transition name="route" mode="out-in">
  <component :is="slotProps.Component"></component>
  </transition>
  </router-view>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue';
export default {
  components: {
    TheHeader,
  },
  created() {
    this.$store.dispatch('tryLogin');
  },
  watch: {
    didAutoLogout(curValue, oldValue){
      if (curValue && curValue !== oldValue) {
        this.$router.replace('/coaches');
      }
    }
  },
  computed: {
    didAutoLogout() {
      return this.$store.getters.didAutoLogout;
    }
  }
};
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>