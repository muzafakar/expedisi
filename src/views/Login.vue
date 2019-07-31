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
                  <h1 class="flex my-4 primary--text">Login markeplace/toko</h1>
                </div>
              </v-card-text>
              <v-form @keyup.enter="login()" @submit="login()">
                <v-text-field
                  name="email"
                  label="Email"
                  prepend-icon="mdi-email"
                  type="email"
                  v-model="auth.username"
                />
                <v-text-field
                  name="password"
                  label="Password"
                  prepend-icon="mdi-lock"
                  type="password"
                  v-model="auth.password"
                />
              </v-form>

              <v-card-actions>
                <v-btn block :loading="loading" color="primary" @click="login()">Login</v-btn>
                <br />
                <v-btn
                  block
                  :loading="loading"
                  color="primary"
                  @click="$router.push('/register')"
                >register</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
// import { setTimeout } from "timers";
import login from "axios";
import { error } from "util";
export default {
  data: () => ({
    loading: false,
    auth: {
      username: "",
      password: "",
      provider: "users"
    }
  }),
  methods: {
    login() {
      this.loading = true;
      login
        .post("http://10.200.179.166/geekcreation/public/api/login", this.auth)
        .then(res => {
          let { access_token } = res.data;
          sessionStorage.setItem("token", access_token);
          this.loading = !this.loading;
          this.$router.push("/dashboard");
        })
        .catch(error => {
          alert("error gan");
        });
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
