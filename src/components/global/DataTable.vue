<template>
  <v-card class="elevation-3">
    <v-toolbar flat color="primary" dark>
      <v-icon>mdi-chart</v-icon>
      <v-toolbar-title>Orderan</v-toolbar-title>
      <v-spacer />
      <v-toolbar-items>
        <v-btn color="primary" small @click="expand = !expand">{{expand ? 'MX' : 'SX'}}</v-btn>
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
          <h4>Jumlah channel: {{props.item.channelCount}}</h4>
          <h4>Iuran Perbulan: Rp. {{props.item.cost}}</h4>
          <h4>Denda: {{props.item.isFined ? 'Rp.' + props.item.fineCharge : '-'}}</h4>
          <h4>Fee Petugas: {{props.item.workerFee}}%</h4>
          <h4>Tanggal Iuran: {{props.item.paymentRange[0] +' - '+ props.item.paymentRange[1]}} (setiap bulannya)</h4>
        </v-card>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    search: "",
    loading: false,
    expand: false,
    headers: [
      { text: "Id Order", align: "left", value: "name" },
      { text: "Username", align: "left", value: "owner" },
      { text: "Tanggal", align: "left", value: "address" }
    ]
  })
};
</script>