<template>
  <v-row class="mr-12 ml-12">
    <v-col v-for="(user, index) in users" :key="index" lg="3" md="4" sm="4">
      <v-card class="d-flex align-center user-card card-shadow">
        <div class="ml-4 mt-6">
          <v-img
            class="rounded-circle border-around"
            width="40"
            height="40"
            :src="user.photo"
          ></v-img>
        </div>
        <div class="data ml-3 mt-6">
          <p>{{ user.name }}</p>
          <p class="text-caption">Última avaliação: {{ updateDate }}</p>
        </div>
      </v-card>
      <v-card class="card-shadow mt-1 d-flex justify-space-between">
        <div class="append d-flex flex-column pt-4 pb-4">
          <p class="text-caption ml-4">{{ user.email }}</p>
          <p class="text-caption ml-4">{{ user.age }} anos {{ user.phone }}</p>
        </div>
        <v-card-actions>
          <v-btn elevation="2" icon class="helper-color"
            ><v-icon>mdi-pencil</v-icon></v-btn
          >
          <v-btn icon
            ><v-icon class="mb-5 helper-color"
              >mdi-settings-helper</v-icon
            ></v-btn
          >
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import eventBus from "@/bus/eventBus";
export default {
  data() {
    return {
      users: []
    };
  },
  computed: {
    updateDate() {
      const date = new Date();
      return `${date.getDate()}/${date.getMonth()}/${date.getFullYear()}`;
    }
  },
  created() {
    const usersArray = JSON.parse(localStorage.getItem("users"));
    if (usersArray) this.users = usersArray;
    eventBus.$on("updateUsers", users => (this.users = users));
  }
};
</script>

<style>
.border-around {
  border: 1px solid white;
}
.user-card {
  height: 6rem;
}
.data > p {
  line-height: 1px;
  text-align: left;
}
.append p {
  height: 3px;
  color: #676767;
}
.card-shadow {
  box-shadow: 0px 5px 5px 0 rgba(0, 0, 0, 0.212) !important;
}
.helper-color {
  color: #290d95 !important;
}
</style>
