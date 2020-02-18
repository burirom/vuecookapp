<template>
  <div>
    <div v-for="cook in cookinfo" :key="cook.id">
      <v-card class="mx-auto cookitem" max-width="600">
        <v-img class="white--text align-end" height="300px" :src="cook.foodImageUrl">
          <v-card-title>{{cook.recipeTitle}}</v-card-title>
        </v-img>
        <v-card-subtitle class="pb-0">Ranking {{cook.rank}}</v-card-subtitle>
        <v-card-text class="text--primary">
          <div>{{cook.recipeDescription}}</div>
        </v-card-text>
        <modal
          :material="cook.recipeMaterial"
          :cookurl="cook.recipeUrl"
          :recipeTitle="cook.recipeTitle"
          :recipeDescription="cook.recipeDescription"
          :img="cook.foodImageUrl"
        ></modal>
      </v-card>
    </div>
  </div>
</template>

<script>
import modal from "./modal";
export default {
  components: {
    modal
  },
  data() {
    return {
      cookinfo: [],
      dialog: false,
      show: false
    };
  },
  created() {
    this.setcookinfo();
  },
  computed: {},
  methods: {
    setcookinfo: function() {
      const axios = require("axios");
      axios({
        method: "GET",
        url:
          "https://rakuten_webservice-rakuten-recipe-v1.p.rapidapi.com/services/api/Recipe/CategoryRanking/20170426",
        headers: {
          "content-type": "application/octet-stream",
          "x-rapidapi-host":
            "rakuten_webservice-rakuten-recipe-v1.p.rapidapi.com",
          "x-rapidapi-key": "2d67331999mshf9aac6941af7895p1c774djsn42a8e2d851a9"
        }
      }).then(response => {
        this.cookinfo = response.data.result;
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.cookitem {
  margin: 50px;
}
</style>