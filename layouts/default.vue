<template>
  <v-app dark>     
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';
export default {
  
  async asyncData() {
    const response = await axios.get('/characters/1009718');
    console.log(response.data.data.results[0]);
    return {
      character: response.data.data.results[0]
    }
  },
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [ ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
    }
},
}
</script>
