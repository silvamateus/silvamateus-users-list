<template>
  <v-row class="card-bg justify-center align-center">
    <v-card class="card-container">
      <div class="white--text pl-4 card-head">
        <v-card-title>Cadastrar Aluno</v-card-title>
      </div>
      <v-form v-model="valid" ref="form">
        <v-row class="pl-8 pr-8 flex-column">
          <v-col>
            <v-text-field
              v-model="name"
              :rules="nameRules"
              label="Nome"
              class="black--text input-height"
              required
            ></v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="Email"
              class="black--text input-height"
              required
            ></v-text-field>
          </v-col>
          <v-col lg="4">
            <v-text-field
              v-model="age"
              label="Idade"
              class="black--text input-height"
              required
            ></v-text-field>
          </v-col>
          <v-col lg="4">
            <v-text-field
              v-model="phone"
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
          <v-col lg="4" class="pt-16 pl-16 ml-16">
            <v-card-actions>
              <v-btn @click="saveUser" class="white--text pl-10 pr-10 btn-color"
                >Salvar</v-btn
              >
            </v-card-actions>
          </v-col>
        </v-row>
      </v-form>
    </v-card>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      name: "",
      nameRules: [v => !!v || "Nome é obrigatório"],
      email: "",
      emailRules: [
        v => !!v || "E-mail é obrigatório",
        v => /.+@.+/.test(v) || "E-mail deve ser valido"
      ],
      age: "",
      phone: ""
    };
  },
  props: {
    showAddUser: {
      type: Boolean
    }
  },
  methods: {
    hideUserModal() {
      this.$emit("hideAddUser", !this.showAddUser);
    },
    saveUser() {
      this.$refs.form.validate();
      const user = {
        name: this.name,
        email: this.email,
        age: this.age,
        phone: this.phone
      };
      let users = [];
      if (localStorage.getItem("users"))
        users = JSON.parse(localStorage.getItem("users"));
      users.push(user);
      localStorage.setItem("users", JSON.stringify(users));
      this.name = "";
      this.email = "";
      this.age = "";
      this.phone = "";
      this.hideUserModal();
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
  height: 70vh;
  width: 50vw;
}
.input-height {
  height: 2.5rem;
}
.cancel-btn {
  color: #341c90 !important;
}
.btn-color {
  background-color: #ff6450 !important;
}
</style>
