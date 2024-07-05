<template>
  <div>
    <div class="contain w-100 h-screen pa-2">
      <div class="boxes h-25 d-flex justify-center align-center ga-2 rounded-xl bg-blue-grey-lighten-4">
        <h1>company Logo</h1>
      </div>
      <div class="boxes h-75 d-flex justify-end flex-column">
        <v-form @submit.prevent="submitForm">
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-text-field v-model="userId" label="User ID (4 digits only)" required></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field v-model="otp" label="OTP (4 digits only)" required></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field v-model="newPassword" label="New Password (at least 6 characters)" type="password" required></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field v-model="confirmPassword" label="Confirm Password" type="password" required></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-btn @click="submitForm" block class="bg-blue text-white">Update</v-btn>
        </v-col>
      </v-row>
    </v-container>

    <v-dialog v-model="dialog" max-width="400">
      <v-card>
        <v-card-title>Registration Status</v-card-title>
        <v-card-text>
          {{ dialogMessage }}
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="dialog = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-form>

      </div>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const userId = ref('');
const otp = ref('');
const newPassword = ref('');
const confirmPassword = ref('');

const dialog = ref(false);
const dialogMessage = ref('');

const submitForm = () => {
  if (!validateUserId() || !validateOTP() || !validatePasswords()) {
    dialogMessage.value = 'Validation failed. Please check the fields.';
    dialog.value = true;
    return;
  }

  dialogMessage.value = 'Registration successful!';
  dialog.value = true;
  // Simulating registration success, navigate to login page after 2 seconds
  setTimeout(() => {
    router.push('/login');
  }, 2000);
};

const validateUserId = () => /^\d{4}$/.test(userId.value);
const validateOTP = () => /^\d{4}$/.test(otp.value);
const validatePasswords = () => newPassword.value.length >= 6 && newPassword.value === confirmPassword.value;
</script>

<style scoped>
/* Add custom styles here if needed */
</style>

<style scoped>
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #fff; /* or any other style you need */
  z-index:1000; /* Ensure it's above other elements */
  transition: bottom 0.3s; /* Smooth transition for better UX */
}
</style>
