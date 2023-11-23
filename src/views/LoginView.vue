<template>
  <v-container fluid>
    <v-overlay :model-value="isLoading" class="align-center justify-center">
      <v-progress-circular
        v-if="isLoading"
        indeterminate
        color="white"
      ></v-progress-circular>
    </v-overlay>
    <v-row justify="center">
      <v-col cols="4">
        <v-card class="pa-8">
          <v-card-title class="text-center">Login Here</v-card-title>
          <v-card-item>
            <v-form @submit.prevent="submit">
              <v-text-field
                type="email"
                prepend-inner-icon="mdi-mail"
                :rules="[rules.required, rules.email]"
                variant="solo"
                v-model="form.email"
                label="Email"
              ></v-text-field>

              <v-text-field
                type="password"
                prepend-inner-icon="mdi-key"
                :rules="[rules.required]"
                variant="solo"
                v-model="form.password"
                label="Password"
              ></v-text-field>

              <v-checkbox
                v-model="form.remember"
                label="Remember Me"
                color="green"
                value="green"
                hide-details
              ></v-checkbox>
              <v-btn
                type="submit"
                block
                class="mt-2"
                color="green-darken-1"
                variant="outlined"
                >Submit
              </v-btn>
            </v-form>
          </v-card-item>

          <v-card-action>
            <div class="mx-4">
              <v-btn block to="/register">Register</v-btn>
            </div>
          </v-card-action>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import { ref } from "vue";

const form = ref({
  email: "",
  password: "",
  remember: false,
});

const isLoading = ref(false);

function submit() {
  isLoading.value = true;

  setTimeout(() => {
    isLoading.value = false;
    alert(JSON.stringify(form.value));
  }, 3000);
}

const rules = {
  required: (value: any) => !!value || "Required.",
  counter: (value: any) => value.length <= 20 || "Max 20 characters",
  email: (value: any) => {
    const pattern =
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return pattern.test(value) || "Invalid e-mail.";
  },
};
</script>

<style scoped></style>
