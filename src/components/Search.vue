<template>
  <v-row class="justify-start pt-12" style="min-width: 80vw">
    <v-col class="d-flex" lg="3" md="3" sm="8">
      <v-text-field
        v-model="usersControl"
        @input="searchUsers"
        label="Busque por nomes ou emails"
        append-icon="mdi-magnify"
        solo
      />
    </v-col>
    <div
      class="d-flex justify-end"
      style="max-width: 56.5vw; min-width: 56.5vw"
    >
      <v-subheader class="pt-6">Filtros: </v-subheader>
      <v-col lg="4">
        <v-select
          lg="3"
          md="3"
          :items="filters"
          v-model="searchFilter"
          solo
          class="d-flex justify-end"
          style="min-width: 7rem;"
          @change="changeSearchFilter"
        ></v-select>
      </v-col>
      <v-col lg="4" class=" d-flex justify-end">
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
      filters: ["todos", "ativos", "inativos"],
      users: [],
      showAddUser: false,
      search: [],
      usersControl: ""
    };
  },
  components: { AddUser },
  methods: {
    hideModal(e) {
      this.showAddUser = e;
    },
    searchCriteria(term) {
      const filter = {
        todos:
          this.users &&
          this.users.filter(
            user => user.name.includes(term) || user.name.includes(term)
          ),
        ativos:
          this.users &&
          this.users.filter(
            user =>
              (user.name.includes(term) || user.name.includes(term)) &&
              user.active
          ),
        inativos:
          this.users &&
          this.users.filter(
            user =>
              (user.name.includes(term) || user.name.includes(term)) &&
              !user.active
          )
      };
      return filter[this.searchFilter];
    },
    searchWithoutText() {
      if (this.searchFilter === "ativos") {
        this.search = this.users && this.users.filter(user => user.active);
      } else if (this.searchFilter === "inativos") {
        this.search = this.users && this.users.filter(user => !user.active);
      } else {
        this.search = this.users && this.users.filter(user => user);
      }
    },
    searchUsers(e) {
      if (e === "") {
        this.searchWithoutText();
      } else {
        this.search = this.searchCriteria(e);
      }
      eventBus.$emit("searchUsers", { search: this.search, searching: true });
    },
    changeSearchFilter() {
      if (this.usersControl === "") {
        this.searchWithoutText();
      } else {
        this.search = this.searchCriteria(this.usersControl);
      }
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
/* Add User Style */
.add-user-btn {
  background-color: #ff6450 !important;
}
</style>
