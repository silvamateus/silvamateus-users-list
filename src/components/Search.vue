<template>
  <v-row class="justify-start pt-12">
    <v-col class="d-flex" lg="3" md="3" sm="8">
      <v-text-field
        @input="searchUsers"
        label="Busque por nomes ou emails"
        append-icon="mdi-magnify"
        solo
      />
    </v-col>
    <div class="d-flex justify-end">
      <v-subheader class="align-self-center">Filtros: </v-subheader>
      <v-col lg="4">
        <v-select
          lg="3"
          md="3"
          :items="filters"
          v-model="searchFilter"
          solo
          class="size-3rem"
          style="min-width: 7rem !important;"
        ></v-select>
      </v-col>
      <v-col lg="4" style="max-width: 20vw">
        <v-btn class="size-3rem add-user-btn white--text"
          ><v-icon>mdi-account-plus</v-icon>
          <span @click="showAddUser = !showAddUser" class="font-weight-bold"
            >novo aluno</span
          >
        </v-btn>
      </v-col>
    </div>
    <v-col v-if="showAddUser">
      <add-user :showAddUser="showAddUser" @hideAddUser="hideModal"
    /></v-col>
  </v-row>
</template>

<script>
import AddUser from "./AddUser.vue";
import eventBus from "@/bus/eventBus";
export default {
  data() {
    return {
      searchFilter: "todos",
      filters: ["todos"],
      users: [],
      showAddUser: false,
      search: []
    };
  },
  components: { AddUser },
  methods: {
    hideModal(e) {
      this.showAddUser = e;
    },
    searchUsers(e) {
      this.search =
        this.users &&
        this.users.filter(
          user => user.name.includes(e) || user.email.includes(e)
        );
      console.log(this.search);
      if (e === "")
        eventBus.$emit("searchUsers", { search: [], searching: false });
      eventBus.$emit("searchUsers", { search: this.search, searching: true });
    }
  },
  created() {
    this.users = JSON.parse(localStorage.getItem("users"));
  }
};
</script>

<style scoped>
/* custom size */
.size-3rem {
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
/* Apply margin */
.margin-right-5rem {
  margin-right: 75px !important;
}
</style>
