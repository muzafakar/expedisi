<template>
  <div>
    <v-app-bar color="primary" dark app>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Marketplace gan</v-toolbar-title>
    </v-app-bar>

    <v-container grid-list-xs>
      <DataTable />
    </v-container>
  </div>
</template>

<script>
import DataTable from "./global/DataTable";
export default {
  components: {
    DataTable
  }
};
</script>
