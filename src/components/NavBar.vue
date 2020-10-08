<template>

    <v-app-bar dense fixed>
      

      <v-toolbar-title class="ma-2" @click="reload"><router-link to="/" >Title</router-link></v-toolbar-title>
      <router-link to="/" ><v-icon class="ma-2 dark">home</v-icon></router-link>

      <v-btn
      class="ma-2"
      outlined
      color="indigo"
      
    ><router-link to="/random" > 
      RANDOM ALBUM
      </router-link>
    </v-btn>

     <div class="text-center">
    <v-menu
      open-on-hover
      top
      offset-y
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
        >
          CATEGORIES
        </v-btn>
      </template>

      <v-list>
        
        <v-list-item
         
        ><v-list-item-content>
          
          <SearchByCategory :category="cd" />
         
         </v-list-item-content>
        </v-list-item>
        <v-list-item
         
        ><v-list-item-content>
          <SearchByCategory :category="vinyl" />
         </v-list-item-content>
        </v-list-item>
        <v-list-item
         
        ><v-list-item-content>
          <SearchByCategory :category="cassette" />
         </v-list-item-content>
        </v-list-item>
        <v-list-item
         
        ><v-list-item-content>
          <SearchByCategory :category="mp3" />
         </v-list-item-content>
        </v-list-item>
        
      </v-list>
    </v-menu>
  </div>

      <v-spacer></v-spacer>

      
    </v-app-bar>
  
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import SearchByCategory from '@/components/SearchByCategory.vue'
@Component({
  components: {
    SearchByCategory,
  }
})
export default class NavBar extends Vue {
}
</script>

