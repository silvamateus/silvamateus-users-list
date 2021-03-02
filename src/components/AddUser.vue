<template>
  <v-row class="card-bg justify-center align-center">
    <v-card class="card-container">
      <div class="white--text pl-4 card-head">
        <v-card-title>Cadastrar Aluno</v-card-title>
      </div>
      <v-form>
        <v-row class="pl-8 pr-8 flex-column">
          <v-col>
            <v-text-field
              label="Nome"
              class="black--text input-height"
            ></v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              label="Email"
              class="black--text input-height"
            ></v-text-field>
          </v-col>
          <v-col lg="4">
            <v-text-field
              label="Idade"
              class="black--text input-height"
            ></v-text-field>
          </v-col>
          <v-col lg="4">
            <v-text-field
              label="Telefone"
              class="black--text input-height"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row class=" justify-space-between">
          <v-col class=" pt-16">
            <v-card-actions>
              <v-btn @click="hideUserModal($event)" text class="cancel-btn"
                >Cancelar</v-btn
              >
            </v-card-actions>
          </v-col>
          <v-col class="pt-16 pl-16 ml-16">
            <v-card-actions>
              <v-btn class="white--text pl-10 pr-10 btn-color">Salvar</v-btn>
            </v-card-actions>
          </v-col>
        </v-row>
      </v-form>
    </v-card>
  </v-row>
</template>

<script>
export default {
  props: {
    showAddUser: {
      type: Boolean
    }
  },
  methods: {
    hideUserModal() {
      this.$emit("hideAddUser", !this.showAddUser);
    }
  }
};
</script>

<style>
.card-bg {
  background: gray !important;
  position: fixed !important;
  height: 100vh !important;
  min-width: 100vw !important;
  left: 0;
  top: 0;
  z-index: 5;
}
.card-head {
  background-color: #290d95 !important;
}
.card-container {
  height: 65vh;
  width: 50vw;
}
.input-height {
  height: 2rem;
}
.cancel-btn {
  color: #341c90 !important;
}
.btn-color {
  background-color: #ff6450 !important;
}
</style>
