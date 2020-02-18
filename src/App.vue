<template>
  <v-app>
    <v-container fluid class="pa-0">
      <v-row align="center">
        <v-col cols="6" sm="6">
          <div class="text-center">
            <div class="my-2">
              <v-btn x-large color="success" dark to="/">ランキング</v-btn>
            </div>
          </div>
        </v-col>
        <v-col cols="6" sm="6">
          <div class="text-center">
            <div class="my-2">
              <v-btn x-large color="success" dark to="/note">ノート</v-btn>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
    <router-view />
  </v-app>
</template>

<script>
// import Home from './views/Home'

export default {
  name: "App",

  components: {
    // Home
  },

  data: () => ({
    //
  })
};
</script>
