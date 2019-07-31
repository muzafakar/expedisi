<template>
  <v-card class="elevation-3">
    <v-toolbar flat color="primary" dark>
      <v-icon>mdi-chart</v-icon>
      <v-toolbar-title>Orderan</v-toolbar-title>
      <v-spacer />
      <v-toolbar-items>
        <v-btn color="primary" @click="modalCreate">
          <v-icon>mdi-plus</v-icon>
        </v-btn>
        <v-text-field
          v-model="search"
          prepend-icon="mdi-magnify"
          clearable
          label="Search"
          color="white"
          single-line
          hide-details
        />
      </v-toolbar-items>
    </v-toolbar>

    <v-data-table
      :headers="headers"
      :items="$store.state.tvkabel"
      :search="search"
      :expand="expand"
    >
      <template v-slot:items="props">
        <tr @click="props.expanded = !props.expanded">
          <td>{{props.item.name}}</td>
          <td>{{generateOwnerName(props.item.ownerId)}}</td>
          <td>{{props.item.address}}</td>
        </tr>
      </template>

      <template v-slot:expand="props">
        <v-card flat class="mx-5 my-2">
          <!-- TODO detail belanjaan disini -->
        </v-card>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    search: "",
    expand: false,
    headers: [
      { text: "Id Order", align: "left", value: "id" },
      { text: "Username", align: "left", value: "name" },
      { text: "Status", align: "left", value: "status" },
      { text: "Tanggal", align: "left", value: "date" }
    ]
  }),
  methods: {
    modalCreate() {
      window.getApp.$emit("MODAL_CREATE");
    }
  }
};
</script>