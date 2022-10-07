<template>
  <v-app>
    <div class="background"></div>
    <v-main class="d-flex justify-center align-center">
      <v-col cols="10" lg="4" class="mx-auto">
        <v-card class="pa-5">
          <div class="text-center">
            <v-avatar size="60" color="grey lighten-2">
              <v-icon size="46" color="primary">mdi-account</v-icon>
            </v-avatar>
            <h2 class="indigo--text">Log in with vuetify</h2>
          </div>
          <v-form ref="form" @submit.prevent="submitedForm">
            <v-card-text>
              <v-text-field
                v-model="password"
                :rules="emailRules"
                type="email"
                label="Email"
                class="blue--text"
                prepend-icon="mdi-account"
              ></v-text-field>
              <v-text-field
                :rules="passwordRules"
                v-model="email"
                :type="passwordShow ? 'text' : 'password'"
                label="Password"
                class="blue--text"
                prepend-icon="mdi-key"
                :append-icon="passwordShow ? 'mdi-eye' : 'mdi-eye-off'"
                @click:append="passwordShow = !passwordShow"
              ></v-text-field>
            </v-card-text>
            <v-card-actions class="justify-center">
              <v-btn
                depressed
                :loading="loading"
                color="primary"
                type="submit"
                class="pa-5"
                >Login</v-btn
              >
            </v-card-actions>
          </v-form>
        </v-card>
      </v-col>

      <v-snackbar v-model="snackbar" top :multi-line="multiLine">
       Logged in successfully!
        <template v-slot:action="{ attrs }">
          <v-btn color="red" text v-bind="attrs" @click="snackbar = false">
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    multiLine:true,
    loading: false,
    snackbar: false,
    passwordShow: false,
    password: "",
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
  }),
  methods: {
    submitedForm() {
      if (this.$refs.form.validate()) {
        this.loading = true;
        setTimeout(() => {
          this.loading = false;
          this.snackbar=true;
          console.log("valid", this.email, this.password);
        }, 3000);
      }
    },
  },
};
</script>

<style>
.background {
  background: blue;
  /* background-image: url("./assets/log.jpg") !important; */
  height: 300px;
  width: 100%;
  display: block;
  position: absolute;
  top: 0;
  background-size: cover;
}
</style>
