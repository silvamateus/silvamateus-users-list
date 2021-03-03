<template>
  <v-row class="mr-16 ml-12" style="max-width: 80vw" v-if="users.length > 0">
    <v-col v-for="(user, index) in users" :key="index" lg="3" md="4" sm="6">
      <v-card class="d-flex align-center user-card card-shadow pl-3 pt-4 ">
        <div>
          <v-img
            class="rounded-circle border-around"
            width="40"
            height="40"
            :src="user.photo"
          ></v-img>
        </div>
        <div class="d-flex flex-column data ml-3">
          <p class="mt-2">{{ user.name }}</p>
          <p class="text-caption">Última avaliação: {{ updateDate }}</p>
        </div>
      </v-card>
      <v-card
        class="card-shadow d-flex justify-space-between mt-1 pt-4 pb-4 pl-4"
      >
        <div class="append d-flex flex-column">
          <p class="text-caption">{{ user.email }}</p>
          <p class="text-caption">{{ user.age }} anos {{ user.phone }}</p>
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
  <v-row v-else class="ml-12">
    <v-col>
      <p>Não há usuários cadastrados</p>
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

<style scoped>
.border-around {
  border: 1px solid white;
}
.user-card {
  height: 6rem;
}
.data > p {
  text-align: left;
  margin: 0;
  padding: 0;
}
.data > p:first-child {
  text-overflow: ellipsis;
  overflow: hidden !important;
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
