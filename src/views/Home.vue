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
import AlbumInfo from '@/components/AlbumInfo.vue'
import AlbumList from '@/components/AlbumList.vue'

@Component({
  components: {
    AlbumList,
  }
})
export default class Home extends Vue {
   
     ids =[12973588,2504814,100,128,159,1239329,2453431,666,750,560];
     sorted_ids:any[]=[];
     sorted_years:any[]=[];
    
    years_list: any[]=[];
    

    getYear (value: any) {
      
      this.years_list.push(value[1]);
      this.sorted_years.push(value[1]);
      this.sorted_ids.push(value[0]);
     
    }
   

    goToSorted() {
        

 
        for( let i=0;i<this.sorted_years.length;i++){
           
            for ( let j=i+1;j<this.sorted_years.length;j++){
                if(this.sorted_years[j]<this.sorted_years[i]){
                    let temp_year = this.sorted_years[i];
                    this.sorted_years[i]=this.sorted_years[j];
                    this.sorted_years[j]=temp_year;
                    let temp_id = this.sorted_ids[i];
                    this.sorted_ids[i]=this.sorted_ids[j];
                    this.sorted_ids[j]=temp_id;
                }
            }
        }
         
        
        
        console.log(this.sorted_ids);
    this.$router.push({ path: 'sorted', query: {
        id_list:this.sorted_ids,
        
    }});
  }
    
}
</script>