<template>
<v-container >
       
    <div >
   
         <v-row no-gutters  >
           
      <v-col
        cols="12"
        sm="4"
        v-for="i in [0,1,2]" :key="i"
      >
        <AlbumCard :album="albums[i]" :show=1 />
        
       </v-col>
       
        </v-row> 
        <v-row no-gutters  >
      <v-col
        cols="12"
        sm="4"
        v-for="i in [3,4,5]" :key="i"
      >
       <AlbumCard :album="albums[i]" :show=1 />
        
       </v-col>
       
        </v-row>
        <v-row no-gutters  >
      <v-col
        cols="12"
        sm="4"
        v-for="i in [6,7,8]" :key="i"
      >
        <AlbumCard :album="albums[i]" :show=1 />
        
       </v-col>
       
        </v-row>
        <v-row no-gutters  >
      <v-col
        cols="12"
        sm="12"
        v-for="i in [9]" :key="i"
      >
        <AlbumCard :album="albums[i]" :show="1" />
        
       </v-col>
       
        </v-row>
    </div>
     <router-link to="/sorted"> <v-btn block @click="goToSorted">
    SORT BY YEAR
    
  </v-btn></router-link>
    </v-container>

</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

import AlbumCard from '@/components/AlbumCard.vue'
import axios from 'axios';
@Component({
  components: {
    
    AlbumCard
  }
})
export default class Home extends Vue {
   
     
     sorted_ids:any[]=[];
     sorted_years:any[]=[];
    albums=[];
    
    years_list: any[]=[];
    baseUrlSearch = 'https://api.discogs.com/database/search?type=release&page=1&per_page=10&key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
    created(){
       
      this.getAlbums();

      
    }
    
    async getAlbums(){
        const response= await axios.get(this.baseUrlSearch);
         this.albums =await response.data.results;
        
    }

   

    goToSorted() {
    this.$router.push({ path: 'sorted', query: {
        albums:this.albums,
        
    }});
  }
    
}
</script>