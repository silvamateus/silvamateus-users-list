<template>
  <v-row v-if="this.users.lengh === 0">
    <v-col>
      <p>Não há usuários cadastrados</p>
    </v-col>
  </v-row>
  <v-row v-else-if="search.search.length === 0 && search.searching">
    <v-col>
      <p>Não há usuários com os critérios de busca utilizado</p>
    </v-col>
  </v-row>
  <v-row style="min-width: 81vw " v-else-if="search.search.length > 0">
    <v-col
      v-for="(user, index) in search.search"
      :key="index"
      lg="3"
      md="4"
      sm="6"
    >
      <user-list :user="user" />
    </v-col>
  </v-row>
  <v-row class="" style="max-width: 81vw" v-else>
    <v-col v-for="(user, index) in users" :key="index" lg="3" md="4" sm="6">
      <user-list :user="user" />
    </v-col>
  </v-row>
</template>

<script>
import eventBus from "@/bus/eventBus";
import UserList from "./UserList.vue";
export default {
  components: { UserList },
  data() {
    return {
      users: [],
      search: { search: [], searching: false }
    };
  },
  created() {
    const usersArray = JSON.parse(localStorage.getItem("users"));
    if (usersArray) this.users = usersArray;
    eventBus.$on("updateUsers", users => (this.users = users));
    eventBus.$on("searchUsers", users => (this.search = users));
  }
};
</script>

<style></style>
