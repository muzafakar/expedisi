<template>
  <v-app id="login" class="primary">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4 lg4>
            <v-card class="elevation-1 pa-3">
              <v-card-text>
                <div class="layout column align-center">
                  <v-avatar size="150" color="red">
                    <img src="../assets/logo.png" alt="admin" />
                  </v-avatar>
                  <h1 class="flex my-4 primary--text">Regisrasi Expedisi</h1>
                </div>
              </v-card-text>
              <v-form @keyup.enter="login()" @submit="login()">
                <v-text-field
                  name="name"
                  label="Nama Expedisi"
                  prepend-icon="mdi-account"
                  type="text"
                  v-model="register.email"
                />
                <v-text-field
                  name="email"
                  label="Email"
                  prepend-icon="mdi-email"
                  type="email"
                  v-model="register.email"
                />
                <v-text-field
                  name="password"
                  label="Password"
                  prepend-icon="mdi-lock"
                  type="password"
                  v-model="register.password"
                />
              </v-form>

              <v-card-actions>
                <v-btn block :loading="loading" color="primary" @click="login()">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import { setTimeout } from "timers";
export default {
  data: () => ({
    loading: false,
    register: {
      email: "",
      password: ""
    }
  }),
  methods: {
    login() {
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
        console.log(this.register.email);
        console.log(this.register.password);
      }, 1500);
    }
  }
};
</script>

<style scoped>
#login {
  height: 50%;
  widows: 100%;
}
</style>