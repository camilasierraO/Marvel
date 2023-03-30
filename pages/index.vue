<head>
  <link href="https://fonts.google.com/specimen/Bangers" rel="stylesheet">
</head>



<template>
  <div class="container">
    <div class="container-top">
      <!-- Contenido del contenedor superior -->
    </div>

    <div class="container-middle">
      <v-slide-group show-arrows>
        <v-slide-item v-for="(character, index) in characters" :key="index">
          <div class="character-card">
            <img :src="character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension" alt="Character image">
            <p class="character-name" >{{ character.name }}</p>
          </div>
        </v-slide-item>
      </v-slide-group>
    </div>

    <div class="container-bottom">
      <!-- Contenido del contenedor inferior -->
    </div>
  </div>
</template>


   <script>
 
    export default {
  
      data() {
        return {
          characters: []
        }
      },
      async mounted() {
      
        const response = await this.$axios.$get('characters',{params:{
          apikey: 'ead4747ffb208c5281361a1be8e8edcd',
          
        }})       
         
        
        this.characters = response.data.results
        
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
    background-color: lightblue;
  }
  
  .container-middle {
    height: 35%;
    background-color: lightgreen;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    padding: 10px;

  }
  
  .container-bottom {
    height: 40%;
    background-color: pink;
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

  }

  .character-name {
    margin-top: 5px;
    color: black;
    font-family: 'Bangers', cursive;
  }




</style>