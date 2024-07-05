<template>
  <div>
    <div class="contain w-100 h-screen pa-2">
      <div class="boxes h-25 d-flex justify-center align-center ga-2 rounded-xl bg-blue-grey-lighten-4">
        <h1>Company Logo</h1>
      </div>
      <div class="boxes h-75 d-flex justify-end flex-column">
        <v-form @submit.prevent="submitForm">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field v-model="userId" label="User ID" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" label="Password" type="password" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-btn @click="submitForm" block class="bg-blue text-white">Login</v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-form>

        <v-dialog v-model="dialog" max-width="400">
          <v-card>
            <v-card-title>Login Status</v-card-title>
            <v-card-text>
              {{ dialogMessage }}
            </v-card-text>
            <v-card-actions>
              <v-btn color="primary" @click="dialog = false">Close</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const userId = ref('');
const password = ref('');

const dialog = ref(false);
const dialogMessage = ref('');

const router = useRouter();

const submitForm = () => {
  if (!validateLogin()) {
    dialogMessage.value = 'Login validation failed. Please check your credentials.';
    dialog.value = true;
    return;
  }

  dialogMessage.value = 'Login successful!';
  dialog.value = true;
  // Simulating login success, navigate to dashboard after 2 seconds
  setTimeout(() => {
    router.push('/dashboard'); // Replace with actual navigation logic
  }, 2000);
};

const validateLogin = () => {
  // Example: Simulate checking credentials
  return userId.value === 'validUserId' && password.value === 'validPassword';
};
</script>

<style scoped>
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #fff; /* or any other style you need */
  z-index: 1000; /* Ensure it's above other elements */
  transition: bottom 0.3s; /* Smooth transition for better UX */
}
</style>
