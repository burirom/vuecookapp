<template>
  <div>
    <div v-for="cook in cookinfo" :key="cook.id">
      <v-card class="mx-auto cookitem" max-width="600">
        <v-img class="white--text align-end" height="300px" :src="cook.img">
          <v-card-title>{{cook.Title}}</v-card-title>
        </v-img>
        <!-- <v-card-subtitle class="pb-0">Ranking {{cook.rank}}</v-card-subtitle> -->
        <v-card-text class="text--primary">
          <div>{{cook.Description}}</div>
        </v-card-text>
        <!-- <modal :material="cook.recipeMaterial" :cookurl="cook.cookurl"></modal> -->
        <notemodal :cookurl="cook.cookurl"/>
      </v-card>
    </div>
  </div>
</template>

<script>
import notemodal from "./notemodal"


export default {
    components:{
        notemodal
    },

  data() {
    return {
      cookinfo: [],
      dialog: false,
      show: false
    };
  },
  created() {
    this.setairtableapp();
  },
  computed: {},
  methods: {
    setairtableapp: function() {
      var Airtable = require("airtable");
      Airtable.configure({
        endpointUrl: "https://api.airtable.com",
        apiKey: "keyvLeIvLfBJLMUCb"
      });
      var base = Airtable.base("appm1gErn3cZ18Qd1");
        var cook = this;
      base("Table 1")
        .select({
          // Selecting the first 3 records in Grid view:
          view: "Grid view",
          
        })
        .eachPage(
          function page(records, fetchNextPage) {
            // This function (`page`) will get called for each page of records.

            records.forEach((record) => {
                let data ={
                   "Title":record.get('Title'),
                   "img":record.get('img'),
                   "cookurl":record.get("cookurl"),
                   "Description":record.get('Description')
                }
            cook.cookinfo.push(data)
            });

            // To fetch the next page of records, call `fetchNextPage`.
            // If there are more records, `page` will get called again.
            // If there are no more records, `done` will get called.
            fetchNextPage();
          },
          function done(err) {
            if (err) {
              return;
            }
          }
        );
    }
  }
};
</script>

<style lang="scss" scoped>
.cookitem {
  margin: 50px;
}
</style>