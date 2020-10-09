<template>
<div class="card"   >
    <v-card
    
    class="mx-auto my-12"
    max-width="374"
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

      

    
    <v-img 
      v-bind:src="getImgSrc()" alt="Artist Picture" max-height="350"
    ></v-img>

    <v-card-title>{{album.title}}</v-card-title>

    <v-card-text>
      

      <div><p><strong>Year: </strong>{{album.year}}</p></div>
    </v-card-text>

   

    <v-divider class="mx-4"></v-divider>
    <v-card-actions v-if="show==1">

      <v-btn
        color="deep-purple lighten-2"
        text
        @click="viewDetails(album)"
        
      >
       Details
      </v-btn>
  
    </v-card-actions>
    
 
  </v-card>
 </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import axios from 'axios';
import ViewDetails from '@/components/ViewDetails.vue'
@Component({
  components: {
    ViewDetails,
  }
})
export default class AlbumCard extends Vue {
    @Prop({required: true}) readonly album!: Object;
    @Prop({required: true}) readonly show: number|undefined;
     @Prop() readonly random: number|undefined;


baseUrl = 'https://api.discogs.com/releases';
  my_key = 'key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  query = '';

  viewDetails(album: any) {
   
    this.$router.push({ path: 'details', query: {
      album_id: album.id,
     
     
    }});
  }

  getImgSrc(){
      if(this.random==1){
          return this.album.images[0].resource_url;
      }else{
      return this.album.cover_image;}
  }


}
</script>