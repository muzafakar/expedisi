<template>
  <v-layout row justify-center>
    <v-dialog
      v-model="formDialog"
      scrollable
      persistent
      max-width="500px"
      transition="dialog-transition"
    >
      <v-card>
        <v-toolbar color="blue darken-3" dark>
          <v-btn icon @click="formDialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>Tambah order</v-toolbar-title>
          <v-spacer />
          <v-toolbar-items>
            <v-btn color="primary" small>Submit</v-btn>
          </v-toolbar-items>
        </v-toolbar>

        <v-card-text>
          <v-container grid-list-md>
            <v-layout row wrap>
              <v-flex xs12>
                <v-text-field name="name" label="Name" required type="text" />
              </v-flex>
              <v-flex xs6>
                <v-text-field
                  name="phone"
                  type="text"
                  label="Phone"
                  required
                  hint="Tidak harus +62"
                />
              </v-flex>
              <v-flex xs6>
                <v-text-field
                  name="email"
                  label="Email"
                  required
                  type="text"
                  hint="Digunakan login di apps"
                />
              </v-flex>
              <v-flex xs12>
                <v-textarea outline name="address" label="Address" required type="text" />
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
      </v-card>
    </v-dialog>

    <v-dialog v-model="progressDialog" scrollable max-width="250px" transition="dialog-transition">
      <v-card color="blue darken-3" dark class="px-3">
        <v-card-title primary-title>
          <strong>Submitting...</strong>
        </v-card-title>
        <v-progress-linear :indeterminate="true" color="white"></v-progress-linear>
      </v-card>
    </v-dialog>
  </v-layout>
</template>


<script>
export default {
  data: () => ({
    formDialog: false,
    progressDialog: false
  }),
  methods: {},
  created() {
    window.getApp.$on("MODAL_CREATE", () => {
      this.formDialog = true;
    });
  }
};
</script>