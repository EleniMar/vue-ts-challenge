<template>
<div class="container text-center" >

<v-container class="grey lighten-5 text-center">
    <v-row no-gutters>
      <v-col
        cols="12"
        sm="6"
      >
        <AlbumCard :album="album" :show=1 :random=1 />
      </v-col>
      <v-col
        cols="12"
        sm="6"
        :key="id"
      >
      <v-card
      class="d-flex grey lighten-5 align-content-center flex-wrap"
      elevation="0"
      min-height="200"
    >
      <v-card
        class="pa-2 grey lighten-5"
        elevation="0"
      ><v-card-title>Discover another album!</v-card-title>
         <v-btn
      class="mx-2"
      fab
      dark
      large
      color="purple"
      @click="reload"
    >
      <v-icon class="ma-3" @click="forceRerender">
        
        autorenew
      </v-icon>


    </v-btn>
    
      </v-card>
    </v-card>
      
      </v-col>
    </v-row>
</v-container>
</div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import AlbumCard from '@/components/AlbumCard.vue'
import axios from 'axios';
@Component({
  components: {
    AlbumCard,
  }
})
export default class Random extends Vue {
  id = Math.floor(Math.random()*15000);
  album=[]
  baseUrl = 'https://api.discogs.com/';
  my_key = '?key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  created(){
    this.getAlbum(this.id);
  }
  async getAlbum(id:any){
    const response = await axios.get(this.baseUrl+'releases/' + id +this.my_key);
    console.log(response);
    this.album=response.data;
  }

  forceRerender(){
    this.id = Math.floor(Math.random()*15000);
    this.getAlbum(this.id);
  }
}
</script>

<style>
.content {
  display: flex;
  justify-content: center;
}

.details-card {
  max-width: 800px;
  padding: 1rem 2rem;
}

.details-card p {
  padding-left: 2rem;
}
</style>