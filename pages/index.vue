<head>
  <link href="https://fonts.google.com/specimen/Bangers" rel="stylesheet">
</head>

<template>
  <div class="container">
    <div class="container-top">
     <center> <img src="@/assets/Captura.png" style="padding-top:10px ;" ></center>
    </div>

    <div class="container-middle">
      <v-slide-group show-arrows>
        <v-slide-item v-for="(character, index) in characters" :key="index" >
          <div class="character-card">
            <img  :src="character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension" alt="Character image"  @click="selectCharacter(character)">
            <p class="character-name" >{{ character.name }}</p>
          </div>
        </v-slide-item>
      </v-slide-group>
    </div>

    <div class="container-bottom d-flex justify-space-between">
  <div class="col1" style="width: 50%;">
    <h2 id="nameSelected">{{ selectedCharacter.name }}</h2>
      <center><img id="imgSelected" :src="selectedCharacter.thumbnail.path + '/portrait_fantastic.' + selectedCharacter.thumbnail.extension" alt="Character image"></center>

  </div>
  <div class="col2 flex-grow-1" style="flex: 1; overflow-y: auto;">
  <h2 class="h2">descripción</h2>
  <p id="descrip">{{ selectedCharacter.description }}</p>
  <br>
  <p>Comics: {{ selectedCharacter.comics.available }}</p>
      <p>Series: {{ selectedCharacter.series.available }}</p>
      <p>Stories: {{ selectedCharacter.stories.available }}</p>
      <p>Events: {{ selectedCharacter.events.available }}</p>
  <br>
  <h2 class="h2">Series del personaje seleccionado</h2>
  <br>
      <ul>
        <li v-for="(serie, index) in series" :key="index">
          <img :src="serie.thumbnail.path + '/portrait_fantastic.' + serie.thumbnail.extension" alt="Serie image">
          <p>{{ serie.title }}</p>
        </li>
      </ul>


</div>

</div>
</div>
</template>


<script>
  export default {
    data() {
      return {
        characters: [],
        selectedCharacter: {
          name: '',
          thumbnail: {
            path: '',
            extension: ''
          },
          comics: { available: 0 },
          series: { available: 0 },
          stories: { available: 0 },
          events: { available: 0 },
          description: ''
        },
       
        series: []

      }
    },
    async mounted() {
      const response = await this.$axios.$get('characters', { params: { apikey: 'ead4747ffb208c5281361a1be8e8edcd' }})
      this.characters = response.data.results
    
    },
    methods: {
      async selectCharacter(character) {
        const response = await this.$axios.$get(`characters/${character.id}`, { params: { apikey: 'ead4747ffb208c5281361a1be8e8edcd' }})
        this.selectedCharacter = response.data.results[0]

     

       
          const seriesResponse = await this.$axios.$get(`characters/${character.id}/series`, { params: { apikey: 'ead4747ffb208c5281361a1be8e8edcd', limit: 3 }})
        this.series = seriesResponse.data.results
} 
      

      
   }
}
</script>

  
<style>
@import url('https://fonts.googleapis.com/css2?family=Bangers&display=swap');

  .container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
  }
  
  .container-top {
    height: 25%;
    background-color: black;
  }
  
  .container-middle {
    height: 35%;
    background-color: black;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    padding: 10px;

  }
  
  .container-bottom {
    height: 40%;
    background-color: white;
    object-fit: cover;
  }
  .character-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    padding: 20px;
    text-align: center;


  }
  .character-card img {
    width: 100%;
    height: 60%;
    object-fit: cover;
    transition: all 0.3s ease-out;

  }

  .character-card:hover {
  transform: scale(1.1);
}

.character-card:hover {
  -webkit-transform: scale(1.1);
  -moz-transform: scale(1.1);
  -ms-transform: scale(1.1);
  -o-transform: scale(1.1);
  transform: scale(1.2);
}

  .character-name {
    margin-top: 5px;
    color: white;
    font-family: 'Bangers', cursive;
  }

  .col1{

    background-color: black;
    overflow: hidden;
    padding: 10px;
    padding-bottom: 40px;
    align-items: center;
    justify-content: center;

    
  }
  .col2{

   background-color: black;
   padding: 5px;

  }


  #imgSelected{
    width: 150px;
    height: 150px;
    text-align: center;
    display: block;
  }
.h2{
  margin-top: 5px;
    color: white;
    font-family: 'Bangers', cursive;
    padding: 5px;
    text-align: center;
    padding-left: 10px;
}

#nameSelected{
  margin-top: 5px;
    color: white;
    font-family: 'Bangers', cursive;
    padding: 5px;
    text-align: center;
    padding-left: 10px;

}



</style>