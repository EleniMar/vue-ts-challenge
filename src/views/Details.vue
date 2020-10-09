<template>
<div class="container text-center" >

<v-container class="grey lighten-5 text-center" :key="i">
    <v-row no-gutters>
      <v-col
        cols="12"
        sm="6"
      >
        <div class="card"   >
    <v-card
    
    class="mx-auto my-12 grey lighten-5 text-center"
    max-width="374"
    elevation="0"
  >
    
    <v-card-text>
      <h2 class=" text--primary">
        {{album.title}}
        </h2>
        <h3>
        <strong>Artist: </strong>
        <p v-for="artist in album.artists" v-bind:key="artist.key">
        {{artist.name}}
        </p>
        </h3>

      <div><p><strong>Year: </strong>{{album.year}}</p></div>
       <div><strong>Genre: </strong>
       <p v-for="genre in album.genres" v-bind:key="genre.key">
        {{genre}}
        </p>
       </div>
        <div><strong>Styles: </strong>
       <p v-for="style in album.styles" v-bind:key="style.key">
        {{style}}
        </p>
       </div>
       <div><p><strong>Country: </strong>{{album.country}}</p></div>


    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-text>
        <div>
             <h3>
        <strong>Tracklist: </strong>
             </h3>
            
          <h5
            v-for="track in album.tracklist"
            :key="track.key"
           
          >

            
             {{track.title}}: {{track.duration}}
            
          </h5>
        
        </div>

    </v-card-text>


  </v-card>
        </div>
  </v-col>

      <v-col
        cols="12"
        sm="6"
      >
      <v-card
      class="d-flex grey lighten-5 align-content-center flex-wrap"
      elevation="0"
      min-height="200"
    >
      <v-card
        class="pa-2 grey lighten-5"
        elevation="0"
      ><v-card-title>Gallery</v-card-title>
      
  <v-carousel v-model="model">
    <v-carousel-item
      v-for="image in album.images"
      :key="image.key"
    >
      <v-sheet
       
        height="100%"
        tile
      >
        <v-row
          class="fill-height"
          align="center"
          justify="center"
        >
          <div class="display-3">
           <v-img
      v-bind:src="image.resource_url" alt="Artist Picture" 
    ></v-img>
          </div>
        </v-row>
      </v-sheet>
    </v-carousel-item>
  </v-carousel>


    
      </v-card>
    </v-card>
      
      </v-col>
    </v-row>
    <h3>You might also like:</h3>
    <v-row
          class="fill-height"
          align="center"
          justify="center"
        :key="i">
        
        <v-col
        cols="12"
        sm="4"
        v-for="recommendation in recommendations" v-bind:key="recommendation.key"
      ><AlbumCard :album="recommendation" :show=0 />
      <v-btn
        color="deep-purple lighten-2"
        text
        @click="viewRecDetails(recommendation)"
        
      >
       Find out more
      </v-btn>
        </v-col>   
            
          
          

    </v-row>
    
    
</v-container>
</div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';
import AlbumCard from '@/components/AlbumCard.vue'
@Component({
  components: {
    AlbumCard,
  }})
export default class Details extends Vue {
  album_id:any;
  i:any;
  album = [];
  recommendations=[];
  baseUrl = 'https://api.discogs.com/releases/';
  baseUrlSearch = 'https://api.discogs.com/database/search?type=release&style='
  my_key = 'key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  recommendationList:any;  
  rerender = "";
 
  created() {
     
    this.album_id = {
      value: this.$route.query.album_id,
   
    };

    
    this.getAlbum(this.album_id.value);
    
    
  }

  async getAlbum(id:any){
    this.i=0;
    this.recommendations=[];
    const response = await axios.get(this.baseUrl + id +'?' +this.my_key);
    this.album = response.data;
    console.log(this.album);
    this.getRecommendations(response.data.styles[this.i],response.data.genres[this.i]);
  }
  
  async getRecommendations(style:any, genre:any){
    const response = await axios.get(this.baseUrlSearch + style +'&' + genre +'&'+this.my_key +'&page=1&per_page=3');
     console.log(response.data.results);
    this.recommendations=response.data.results;
    
    
  }
  viewRecDetails(album: any) {
   
   this.album=album;
  this.getAlbum(album.id);
   this.i=1;
  }
 
}
</script>

<style>

</style>