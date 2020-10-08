<template>

  <router-link to="/cd">
    <v-btn @click="getAlbums(category)">
     
     {{category}}
      
    </v-btn>
  </router-link>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import axios from 'axios';
import AlbumList from '@/components/AlbumList.vue'

@Component({
  components: {
    AlbumList,
  }
})
export default class SearchByCategories extends Vue {
     @Prop({required: true}) readonly category!: string;
    

    baseUrlSearch = 'https://api.discogs.com/database/search?type=release&format=cd';
  baseUrl = 'https://api.discogs.com/';
  my_key = 'key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  query = '';

    albums:any;
    ids: any[]=[];
    created(){
        
    }

     sendAlbums(category:string) {
    
    this.$router.push({ path: category, query: {
      ids: this.ids
     
    }});
  }
   
    async getAlbums(){
        const response = await axios.get(this.baseUrlSearch +'&page=1&per_page=10&'+this.my_key);
        
        this.albums=response;
        this.albums.data.results.forEach((element: any) => {
            this.ids.push(element.id);
            console.log(element.id);
        });

    }
}
</script>