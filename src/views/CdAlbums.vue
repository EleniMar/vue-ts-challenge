<template>
<div >
  <AlbumList :ids="ids" />
    <v-btn @click="goToSorted">
     
      Sort by year
      
    </v-btn>
</div>
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
export default class CdAlbums extends Vue {
    
    
     sorted_ids:any[]=[];
     sorted_years:any[]=[];
    
    years_list: any[]=[];
    baseUrlSearch = 'https://api.discogs.com/database/search?type=release&format=cd';
  baseUrl = 'https://api.discogs.com/';
  my_key = 'key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  query = '';

    results:any;
    ids:any;
    created(){
       this.ids = this.$route.query.ids;
   
    }
}
</script>