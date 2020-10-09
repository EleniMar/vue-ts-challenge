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
        <router-link to="/">    <v-btn block @click="goToSorted">
    BACK
   
  </v-btn> </router-link>
    </v-container>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import AlbumCard from '@/components/AlbumCard.vue'


@Component({
  components: {
    AlbumCard,
  }
})
export default class SortedCards extends Vue {
    albums:any;
    
    
    created(){
        
        this.albums=this.$route.query.albums;
       
        for(let i=0;i<this.albums.length;i++){
          for(let j=i+1;j<this.albums.length;j++){
            if(this.albums[j].year<this.albums[i].year){
              let temp = this.albums[i];
              this.albums[i] = this.albums[j];
              this.albums[j]=temp;
            }
          }
        }
        
        
        
    }

    
}
</script>