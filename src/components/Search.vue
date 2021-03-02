<template>
  <v-row class="d-flex justify-space-between  mt-13">
    <v-col class="d-flex ml-15 mt-6" lg="3" md="3">
      <v-text-field
        class="size-1-5rem rounded-0"
        style="border-top-right-radius: .3rem !important; border-bottom-right-radius: .3rem !important;"
        label="Busque por nomes ou emails"
        solo
      />
      <v-btn
        color="white"
        style="border-top-right-radius: .3rem !important; border-bottom-right-radius: .3rem !important;"
        class="size-1-5rem search-bar rounded-0"
        ><v-icon>mdi-magnify</v-icon></v-btn
      >
    </v-col>
    <v-col lg="8" md="6">
      <v-row class="margin-right-5rem justify-end">
        <v-subheader class="align-self-center mt-6">Filtros: </v-subheader>
        <v-col lg="4">
          <v-select
            lg="3"
            md="3"
            sm="3"
            :items="filters"
            v-model="searchFilter"
            solo
            class="size-1-5rem mt-6 margin-left-n5rem"
            style="min-width: 7rem !important;"
          ></v-select>
        </v-col>
        <v-col class="mr-12 d-flex justify-center" lg="4">
          <v-btn class="mt-6 mr-16 size-1-5rem add-user-btn white--text"
            ><v-icon>mdi-account-plus</v-icon>
            <span
              @click="showAddUser = !showAddUser"
              class="ml-1 font-weight-bold"
              >novo aluno</span
            >
          </v-btn>
        </v-col>
      </v-row>
    </v-col>
    <v-col v-if="showAddUser">
      <add-user :showAddUser="showAddUser" @hideAddUser="hideModal"
    /></v-col>
  </v-row>
</template>

<script>
import AddUser from "./AddUser.vue";
export default {
  data() {
    return {
      searchFilter: "todos",
      filters: ["todos"],
      users: [],
      showAddUser: false
    };
  },
  components: { AddUser },
  methods: {
    hideModal(e) {
      this.showAddUser = e;
    }
  },
  created() {
    this.users = localStorage.getItem("users");
  }
};
</script>

<style scoped>
/* custom size */
.size-1-5rem {
  height: 3rem !important;
}
/* Set position relative */
.position-relative {
  position: relative !important;
}
/* Search bar style */
.search-bar {
  right: 8px;
  border: 0 !important;
  box-shadow: 5px 5px 5px -4px rgba(0, 0, 0, 0.2),
    0 6px 5px -5px rgba(0, 0, 0, 0.42) !important;
}
/* Add User Style */
.add-user-btn {
  background-color: #ff6450 !important;
}
/* Apply negative margin */
.margin-right-5rem {
  margin-right: 75px !important;
}
</style>
