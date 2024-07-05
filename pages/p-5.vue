<template>
    <div>
      <div class="container w-100 h-screen d-flex flex-column ga-3 pa-2">
        <div class="boxex box1 pa-2 d-flex justify-center align-center rounded-lg bg-blue-grey-lighten-5">
          <h1>Company logo</h1>
        </div>
        <div class="boxex pa-2 h-screen">
          <v-sheet class="w-100">
      <v-form fast-fail @submit.prevent>
        <v-text-field
          label="User Id"
        ></v-text-field>
        <div class="success-box pa-2 w-100 bg-blue-grey-lighten-5 d-flex flex-column align-center justify-space-between">
            <h1 class="text-red-darken-2 text-lg ">Failure</h1>
            <h2 class="text-center">New Password Not Matching Required</h2>
            <h3 class="text-center">Uppercase Lowercase Number</h3>
        </div>
  
      <v-btn class="mt-3 bg-indigo-accent-2" type="submit" block>Updates</v-btn>
      </v-form>
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