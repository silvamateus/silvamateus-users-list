<template>
  <v-row class="card-bg justify-center align-center">
    <v-card class="card-container">
      <div
        class="white--text card-head d-flex align-center justify-space-between pr-8"
      >
        <v-card-title>Cadastrar Aluno</v-card-title>
        <span @click="hideUserModal" class="pointer">x</span>
      </div>
      <v-form
        v-model="valid"
        ref="form"
        @submit.prevent="saveUser"
        lazy-validation
        class="pl-6 pr-6"
      >
        <v-row class="flex-column">
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
              :rules="ageRules"
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
          <v-col class="">
            <v-card-actions>
              <v-btn @click="hideUserModal()" text class="cancel-btn"
                >Cancelar</v-btn
              >
            </v-card-actions>
          </v-col>
          <v-col lg="4" class="">
            <v-card-actions>
              <v-btn type="submit" class="white--text pl-10 pr-10 btn-color"
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
import eventBus from "@/bus/eventBus";
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
      ageRules: [
        v => !!v || "Idade é obrigatória",
        v => !isNaN(parseInt(v)) || "Idade deve ser número"
      ],
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
    async saveUser() {
      if (this.$refs.form.validate()) {
        const user = {
          name: this.name,
          email: this.email,
          age: this.age,
          phone: this.phone,
          photo: "",
          active: true
        };
        await fetch("https://randomuser.me/api/", {
          method: "GET"
        })
          .then(response => response.json())
          .then(
            response => (user.photo = response.results[0].picture.thumbnail)
          )
          .catch(err => console.error(err));
        let users = [];
        if (localStorage.getItem("users"))
          users = JSON.parse(localStorage.getItem("users"));
        await users.push(user);
        await localStorage.setItem("users", JSON.stringify(users));
        this.name = "";
        this.email = "";
        this.age = "";
        this.phone = "";
        this.hideUserModal();
        await eventBus.$emit("updateUsers", users);
      }
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
.pointer {
  cursor: pointer;
}
</style>
