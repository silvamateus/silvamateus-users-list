<template>
  <v-main>
    <search />
    <users-list />
  </v-main>
</template>

<script>
import Search from "./Search.vue";
import UsersList from "./UsersList.vue";
export default {
  name: "MainContainer",
  components: {
    Search,
    UsersList
  }
};
</script>

<style></style>
