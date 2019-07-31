<template>
  <v-data-table :headers="headers" :items="desserts" sort-by="calories" class="elevation-1">
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-toolbar-title>Orderan Gan</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on }">
            <v-btn color="primary" dark class="mb-2" v-on="on">New Item</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container grid-list-md>
                <v-layout wrap>
                  <v-flex xs12 sm12 md12>
                    <v-text-field v-model="editedItem.username" label="Email penerima"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm12 md12>
                    <v-text-field v-model="editedItem.alamat" label="Alamat pengiriman"></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm6 md4>
                    <v-select
                      v-model="editedItem.id"
                      :items="produk"
                      item-text="nama_produk"
                      item-value="id"
                      label="pilih barang"
                    ></v-select>
                  </v-flex>
                  <!-- <v-flex xs12 sm6 md4>
                    <v-select :items="parseBarangName" label="Barang 3"></v-select>
                  </v-flex>-->
                </v-layout>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="save()">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.action="{ item }">
      <v-btn @click="showDetail(item)" color="primary">Detail</v-btn>
      <v-btn @click="kirimBarang(item)" color="primary">Kirim</v-btn>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
import a from "axios";
export default {
  data: () => ({
    dialog: false,
    barangs: [
      {
        id: "idBarang",
        nama: "NamaBarang",
        detail: "OtherDetails..."
      },
      {
        id: "idBarang",
        nama: "NamaBarang3",
        detail: "OtherDetails..."
      },
      {
        id: "idBarang",
        nama: "NamaBarang2",
        detail: "OtherDetails..."
      }
    ],
    headers: [
      {
        text: "ID Order",
        align: "left",
        sortable: false,
        value: "id"
      },
      { text: "Nama Penerima", value: "username" },
      { text: "Email", value: "email" },
      { text: "Status", value: "status" },
      { text: "Actions", value: "action", sortable: false }
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      id: "",
      username: "",
      alamat: "",
      email: "",
      status: ""
    },
    defaultItem: {
      id: "",
      alamat: "",
      username: "",
      email: "",
      status: ""
    },
    produk: null
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },

    parseBarangName() {
      const barangNames = [];

      this.produk.forEach(function(element) {
        barangNames.push(element.nama_produk);
      });

      return barangNames;
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    }
  },

  created() {
    this.initialize();
  },
  mounted() {
    this.getProduk();
  },
  methods: {
    getProduk() {
      a.get("http://10.200.179.166/geekcreation/public/api/produk/all").then(
        res => {
          let { data } = res;
          this.produk = data;
          console.log(this.produk);
        }
      );
    },
    initialize() {
      this.desserts = [
        {
          id: "ASDF12",
          username: "GGWP",
          email: "email@provider.com",
          status: "Belum Terkirim"
        }
      ];
    },

    showDetail(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    kirimBarang(item) {
      // TODO post new orderang status
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.editedItem.status = "dikirim";
      this.desserts.push(this.editedItem);
    },

    deleteItem(item) {
      const index = this.desserts.indexOf(item);
      confirm("Are you sure you want to delete this item?") &&
        this.desserts.splice(index, 1);
    },

    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },

    save() {
      console.log(this.editedItem);
      // if (this.editedIndex > -1) {
      //   Object.assign(this.desserts[this.editedIndex], this.editedItem);
      // } else {
      //   this.editedItem.id = "randomID";
      //   this.desserts.push(this.editedItem);
      // }
      // this.close();
    }
  }
};
</script>