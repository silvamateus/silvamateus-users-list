<template>
  <v-row class="d-flex justify-space-around">
    <v-col class="d-flex ml-4 mt-4" lg="3" md="3" sm="3">
      <v-text-field
        class="size-1-5rem rounded-0"
        style="border-top-right-radius: .3rem !important; border-bottom-right-radius: .3rem !important;"
        label="Busque por nomes ou emails"
        solo
      />
      <v-btn
        style="border-top-right-radius: .3rem !important; border-bottom-right-radius: .3rem !important;"
        class="size-1-5rem search-bar rounded-0"
        ><v-icon>mdi-magnify</v-icon></v-btn
      >
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      searchFilter: "todos",
      filters: ["todos"],
      users: []
    };
  },
  created() {
    this.users = localStorage.getItem("users");
  }
};
</script>

<style>
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
  background: white !important;
  border: 0 !important;
  box-shadow: 5px 5px 5px -4px rgba(0, 0, 0, 0.2),
    0 6px 5px -5px rgba(0, 0, 0, 0.42) !important;
}
</style>
