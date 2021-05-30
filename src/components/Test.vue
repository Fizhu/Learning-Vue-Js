<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app clipped>
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Dashboard</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-cog</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Stock Management</v-toolbar-title>
    </v-app-bar>

    <v-content style="padding: 16px 16px 16px 16px;">
      <v-container fluid class="align-start">
        <v-row dense>
          <v-col v-for="datum in data" :key="datum.id_barang" :cols="3">
            <v-card v-ripple style="margin: 8px 8px 8px 8px;">
              <v-img
                :src="datum.foto"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title v-text="datum.nama_barang"></v-card-title>
              </v-img>
              <v-card-text class="text--primary">
                <div v-text="datum.keterangan"></div>
              </v-card-text>
              <v-card-text>
                <div v-text="datum.tanggal_masuk"></div>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn icon>
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
                <v-btn icon>
                  <v-icon>mdi-brush</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <!-- </div> -->
    </v-content>
    <v-footer app>
      <span>&copy; GABUT 2020</span>
    </v-footer>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  props: {
    source: String
  },
  data: () => ({
    drawer: null,
    data: []
  }),
  created() {
    this.$vuetify.theme.dark = true;
  },
  mounted() {
    this.load();
  },
  methods: {
    submitLogin() {
      let username = this.data.username;
      let pw = this.data.pw;
      axios.post(Endpoint.login, {
        username: username,
        password: pw
       })
      .then(function (response) {
         //todo handle response
         console.log("onResponse" + response);
       })
    .catch(function (error) {
        //todo handle error
        console.log("onError" + error);
       });
    }
    load() {
      let url = "https://bus.unila.ac.id/crud/api/v1/getlistbarang.php";
      axios
        .get(url)
        .then(res => {
          this.data = res.data.data;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>
