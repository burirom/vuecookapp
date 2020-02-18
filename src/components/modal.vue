<template>
  <div>
    <v-card-actions>
      <v-btn color="success" dark @click="setairtableapp()">ノートに保存</v-btn>
      <v-spacer></v-spacer>
      <v-btn color="success" dark :href="cookurl">作り方</v-btn>

      <v-btn color="success" dark outlined @click="show = !show">
        材料
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>
    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          <h2>材料</h2>
          <ul v-for="cookmaterial in this.material" :key="cookmaterial.id">
            <li>{{cookmaterial}}</li>
          </ul>
        </v-card-text>
      </div>
    </v-expand-transition>
  </div>
</template>

<script>
export default {
  props: {
    // material: {
    //   type:Array,
    //   required: true
    // },
    cookurl: {
      type: String,
      required: true
    },
    recipeTitle: {
      type: String,
      required: true
    },
    recipeDescription: {
      type: String,
      required: true
    },
    img: {
      type: String,
      required: true
    },

  },

  data() {
    return {
      show: false
    };
  },
  methods: {
    setairtableapp: function() {
      var Airtable = require("airtable");
      Airtable.configure({
        endpointUrl: "https://api.airtable.com",
        apiKey: "keyvLeIvLfBJLMUCb"
      });
      var base = Airtable.base("appm1gErn3cZ18Qd1");

      base("Table 1").create(
        [
          {
            fields: {
              "Title":this.recipeTitle,
              "img":this.img,
              "cookurl":this.cookurl,
              "Description":this.recipeDescription,
             

            }
          },
         
        ],
        function(err) {
          if (err) {
          
            return;
          }
        }
      );


    }
  }
};
</script>

<style>
</style>