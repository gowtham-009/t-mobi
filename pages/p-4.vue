<template>
    <div>
      <div class="container w-100 h-screen d-flex flex-column ga-3 pa-2">
        <div class="boxex box1 pa-2 d-flex justify-center align-center rounded-lg bg-blue-grey-lighten-5">
          <h1>Company logo</h1>
        </div>
        <div class="boxex pa-2 h-screen">
          <v-sheet class="w-100 h-screen d-flex flex-column justify-space-between " style="border: 2px solid red;">
      <v-form fast-fail @submit.prevent>
        <v-text-field
          
          label="User Id"
        ></v-text-field>
        <div class="success-box pa-2 w-100 bg-blue-grey-lighten-5 d-flex flex-column align-center justify-space-between">
            <h1 class="text-purple-darken-4 text-lg">Success</h1>
            <h3>New Password Updated</h3>
        </div>
      </v-form>
    <v-btn class="mb-3 bg-indigo-accent-2 flex-0-0" type="submit" block>Log in</v-btn>
   
    </v-sheet>
  
        </div>
      </div>
    </div>
  </template> 
  <style>
  
  .box1{
    height:230px;
  }
  .success-box{
    height: 250px;
  }
  </style>