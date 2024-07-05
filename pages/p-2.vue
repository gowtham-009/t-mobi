<template>
    <div>
      <div class="container w-100 h-screen d-flex flex-column ga-2 pa-2">
        <div class="boxex">
          <logo/>
        </div>
        <div class="boxex pa-1 h-screen">
          <v-container class="pa-0">
            <v-row no-gutters>
              <v-col>
                <v-sheet class="ma-1">
                  <div class="new-loan w-100 pa-2 d-flex justify-start bg-green-lighten-1 rounded-lg">
                    <h1>New<br>loan</h1>
                  </div>
                </v-sheet>
              </v-col>
              <v-col>
                <v-sheet class="ma-1">
                  <div class="new-loan w-100 pa-2 d-flex justify-start bg-green-lighten-1 rounded-lg">
                    <h1>New<br>user</h1>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
  
            <v-row no-gutters>
              <v-col cols="15">
                <v-sheet class="ma-1">
                  <div class="srh-btn w-100 d-flex justify-center align-center bg-yellow-darken-1 rounded-lg">
                    <h1 style="color: white;">Search and Close</h1>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
  
            <v-row no-gutters>
              <v-col cols="15">
                <v-sheet class="ma-1">
                  <div class="srh-btn w-100 d-flex justify-center align-center bg-light-blue-darken-4 rounded-lg">
                    <h1 style="color: white;">Admin</h1>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
  
            <v-row no-gutters>
              <v-col>
                <v-sheet class="ma-1">
                  <div class="new-loan w-100 pa-2 d-flex justify-end align-end bg-light-blue-accent-2 rounded-lg">
                    <h1 style="color: white; text-align: right;">Leadger<br>Report</h1>
                  </div>
                </v-sheet>
              </v-col>
              <v-col>
                <v-sheet class="ma-1">
                  <div class="new-loan w-100 pa-2 d-flex justify-end align-end bg-light-blue-accent-2 rounded-lg">
                    <h1 style="color: white; text-align: right;">Balance<br>Check</h1>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
  
            <v-row no-gutters style="display: flex; justify-content: end;">
              <v-col cols="6">
                <v-sheet class="ma-1">
                  <div class="srh-btn w-100 pa-2 d-flex justify-end align-center bg-black rounded-lg">
                    <h1 style="color: white; text-align: right;">log out</h1>
                  </div>
                </v-sheet>
              </v-col>
            </v-row>
  
          </v-container>
        </div>
      </div>
  
    </div>
  </template>
  
  <script>
  // Importing the logo component
  import logo from "~/components/logo.vue";
  
  export default {
    components: {
      logo,
    },
  };
  </script>
  
  <style scoped>
  .new-loan {
    height: 200px;
  }
  
  .srh-btn {
    height: 70px;
  }
  </style>
  