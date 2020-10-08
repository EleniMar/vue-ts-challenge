<template>
 <div :key="album.id">
     
    
      <v-btn
        color="deep-purple lighten-2"
        text
        @click="viewDetails(album)"
        
      >
       Details
      </v-btn>
  
 </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import axios from 'axios';
@Component
export default class ViewDetails extends Vue {
    @Prop({ required: true })
  readonly album:{
      
    }|undefined;
     
     public set rec(value: any) {
    this.recommendations=value;
  }
    
   baseUrlSearch = 'https://api.discogs.com/database/search?type=master&style=';
  baseUrl = 'https://api.discogs.com/';
  my_key = 'key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  query = '';
  
  tracklist:any;
  imageList:any;
  recommendations:any;
    
   created() {
    this.getDetails(this.album);
    
    
  }

  async getDetails(album:any){
    let response:any;
    response = await axios.get(this.baseUrl+'releases/' + album.id +'?'+this.my_key);
    this.tracklist = this.getTrackList(album.tracklist);
    this.imageList = this.getImgList(album.images);
    const r = this.getRec(album.styles[0]);
    r.then((value)=>{
      this.recommendations=value;
      
    }
    )
  
    
  }

    getTrackList(album_l:any){
    let list: any[]=[];
    album_l.forEach((element: any) => {
     list.push(element.title)
    });

       return list;
  }

  getImgList(album_l:any){
    let list: any[]=[];
    album_l.forEach((element: any) => {
     list.push(element.resource_url);
    });
      return list;
  }
 
  
    async getRec(style:any){
   const response = await axios.get(this.baseUrlSearch+style +'&page=1&per_page=3&'+this.my_key);
   const list = response.data.results;
  return list;
  
   
    }

    viewDetails(album: any) {
    console.log(this.recommendations);
    this.$router.push({ path: 'details', query: {
      album_id: album.id,
      artist_id: album.artists[0].id,
      title: album.title,
      artist: album.artists[0].name,
      year: album.year,
      country: album.country,
      images: this.imageList,
      genres: album.genres[0],
      styles:album.styles[0],
      tracklist: this.tracklist,
      recommendations:this.recommendations,
     
    }});
  }

 
}
</script>