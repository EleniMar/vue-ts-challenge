<template>
 <div class="card"   >
    <v-card
    :loading="loading"
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
      v-bind:src="getImgSource()" alt="Artist Picture" 
    ></v-img>

    <v-card-title>{{title}}</v-card-title>

    <v-card-text>
      <p class="display-1 text--primary">
        <strong>Artist: </strong>
        {{album.artists[0].name}}
      </p>

      <div><p><strong>Year: </strong>{{year}}</p></div>
      <div><p><strong>Genre: </strong>{{album.styles[0]}}</p></div>
    </v-card-text>

   
  </v-card>
 </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class RecommendationsInfo extends Vue {
    @Prop({required: true}) readonly id: number|undefined
  
    @Prop(String)  title: string|undefined
    
    @Prop({ default: 0 })
  private _year: number|undefined;
  public get year(): number|undefined {
    return this._year;
  }
  public set year(value: number|undefined) {
    this._year=value;
  }
 
    created() {
    this.getAlbum(this.id);
    
    
  }

  baseUrl = 'https://api.discogs.com/';
  my_key = '?key=FMvTlSGADQWmohiXndNO&secret=zaYzcFPxvIEZaQJeXpwhJDdPlHQYNTaR';
  query = '';
  img_src = '';


  
  album:any;
  
   async getAlbum(id: any){
    
    let response:any;
    while(true){
      
      response = await axios.get(this.baseUrl+'releases/' + id +this.my_key);
      
      if(response.data!=null){
        
        break;
      }
      
    }
    
    
    this.album=(response.data);
 
    this.img_src = this.album.images[0].resource_url;
    this.year = this.album.year;
    
    this.title = this.album.title;
    
     
    this.$emit( 'sendYear',[this.id,this.year]);
     
  }


 
 
  getImgSource(){
        return this.img_src;
    }
  



 
}
</script>