<template>
  <div>
    <v-card-actions>
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
        <!-- <v-btn color="success" dark>保存</v-btn> -->
      </div>
    </v-expand-transition>
  </div>
</template>

<script>
export default {
  props: {
    material:{
       
    },
    cookurl: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      show: false
    };
  }
};
</script>

<style>
</style>