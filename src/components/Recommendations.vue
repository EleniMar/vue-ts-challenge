<template>
<v-container>
     <v-row no-gutters>
      <v-col
        cols="12"
        sm="4"
      >
    <RecommendationsInfo :id="recommendations[0].id"  />
      </v-col>
       
      <v-col
        cols="12"
        sm="4"
      >
    <RecommendationsInfo :id="recommendations[1].id"   />
      </v-col>
      
      <v-col
        cols="12"
        sm="4"
      >
    <RecommendationsInfo :id="recommendations[2].id" />
      </v-col></v-row>
</v-container>
</template>
<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

import RecommendationsInfo from '@/components/RecommendationsInfo.vue'
@Component({
  components: {
    RecommendationsInfo,
  }
})export default class Recommendations extends Vue {
    @Prop({ required: true })
  readonly recommendations: Object|undefined;

created() {
    this.getRecommendations(this.recommendations);
    
    
  }
getRecommendations(list:any){
    console.log(list);
}




}



  </script>