<template>
  <div>
    <v-app-bar color="primary" dark app>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Marketplace gan</v-toolbar-title>
    </v-app-bar>

    <ModalCreate />

    <v-container grid-list-xs>
      <DataTable />
    </v-container>
  </div>
</template>

<script>
import DataTable from "./global/DataTable";
import ModalCreate from "./global/ModalCreate";
export default {
  components: {
    DataTable,
    ModalCreate
  }
};
</script>
