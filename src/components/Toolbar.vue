<template>
  <v-card class="overflow-hidden">
    <v-app-bar class="white--text rounded-0 toolbar-container" flat app>
      <v-row class="box d-flex justify-end">
        <v-col lg="4" class="d-flex">
          <div
            class="toolbar-card rounded-0 white--text d-flex align-center pl-2rem position-relative"
          >
            <div>
              <v-img
                class="rounded-circle border-around"
                width="40"
                height="40"
                lazy-src="https://images.generated.photos/NDJMRXVcwlvoH9KdFjO5PpL1lAz-G7j2QEnKux836Ss/rs:fit:512:512/wm:0.95:sowe:18:18:0.33/Z3M6Ly9nZW5lcmF0/ZWQtcGhvdG9zL3Yz/XzA5NTE3OTIuanBn.jpg"
                src="https://images.generated.photos/NDJMRXVcwlvoH9KdFjO5PpL1lAz-G7j2QEnKux836Ss/rs:fit:512:512/wm:0.95:sowe:18:18:0.33/Z3M6Ly9nZW5lcmF0/ZWQtcGhvdG9zL3Yz/XzA5NTE3OTIuanBn.jpg"
              ></v-img>
            </div>
            <div class=" user-info">
              <p class=" text-caption">NOME</p>
              <p class=" text-caption">Último login</p>
            </div>
            <v-btn flat class="btn-absolute">
              <v-icon>mdi-menu-down</v-icon>
            </v-btn>
          </div>
        </v-col>
      </v-row>
      <v-spacer></v-spacer>
    </v-app-bar>
  </v-card>
</template>

<script>
export default {
  name: "Toolbar"
};
</script>

<style>
/* Put Box shadow in the sides of the container */
.box::before,
.box::after {
  content: " ";
  height: 116%;
  position: absolute;
  top: 0;
  width: 15px;
  margin: -5px;
}
.box::before {
  box-shadow: inset -15px 0 15px -15px rgba(0, 0, 0, 0.288);
  left: -15px;
}
.box::after {
  box-shadow: inset 15px 0 15px -15px rgba(0, 0, 0, 0.288);
  right: 32px;
}
.box {
  height: 100%;
  width: 70vw;
  position: relative;
  margin-left: 3rem !important;
}
/* Toolbox Container: 
  set Background
  set card gradient 
  set Left box shadow */
.toolbar-container {
  background-color: #ff6450 !important;
}
.toolbar-card {
  background: linear-gradient(#ff6551, #f68e81) !important;
  margin: -15px -30px;
  position: relative;
  height: calc(100% + 1.9rem);
  width: 100%;
}
.toolbar-card::before {
  content: " ";
  width: 15px;
  position: absolute;
  top: 0;
  box-shadow: inset -15px 0 15px -15px rgba(0, 0, 0, 0.288);
  left: -15px;
  height: 100%;
}
/* Custom CSS adjusts */
.border-around {
  border: 1px solid white;
}
.pl-2rem {
  padding-left: 2rem;
}
.position-relative {
  position: relative !important;
}
.btn-absolute {
  position: absolute !important;
  height: 100% !important;
  right: 0px;
  background: linear-gradient(#ff6551, #f68e81) !important;
}

/* Align and set heights of user card */
.user-info {
  padding-left: 0.5rem;
}
.user-info p {
  height: 1px;
}
.user-info > p:first-child {
  font-weight: 600;
}
</style>
