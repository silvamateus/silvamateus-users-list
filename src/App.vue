<template>
  <v-app>
    <toolbar></toolbar>
    <main-container class="pl-12" />
  </v-app>
</template>

<script>
import MainContainer from "./components/MainContainer.vue";
import Toolbar from "./components/Toolbar.vue";
export default {
  name: "App",
  components: {
    Toolbar,
    MainContainer
  },
  data: () => ({
    //
  })
};
</script>

<style>
* {
  box-sizing: border-box;
}
</style>
