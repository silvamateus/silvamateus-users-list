<template>
  <div>
    <v-card class="d-flex align-center user-card card-shadow pl-3 pr-2">
      <div class="pr-2">
        <v-img
          class="rounded-circle border-around"
          width="40"
          height="40"
          :src="user.photo"
        ></v-img>
      </div>
      <div class="d-flex flex-column data">
        <p class="">{{ user.name }}</p>
        <p class="text-caption">Última avaliação: {{ updateDate }}</p>
      </div>
    </v-card>
    <v-card class="card-shadow d-flex justify-space-between pl-3 pb-2">
      <div class="append d-flex flex-column">
        <p class="text-caption">{{ user.email }}</p>
        <p class="text-caption">{{ user.age }} anos {{ user.phone }}</p>
      </div>
      <v-card-actions>
        <v-btn elevation="2" icon class="helper-color" :disabled="!user.active"
          ><v-icon>mdi-pencil</v-icon></v-btn
        >
        <v-btn icon :disabled="!user.active"
          ><v-icon class="helper-color">mdi-settings-helper</v-icon></v-btn
        >
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    user: [Array, Object]
  },
  computed: {
    updateDate() {
      const date = new Date();
      return `${date.getDate()}/${date.getMonth()}/${date.getFullYear()}`;
    }
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
