<template>
    <div class="characters-container">
      <h1>Personajes de Marvel</h1>
      <div class="characters-list">
        <div v-for="character in characters" :key="character.id" class="character-card">
          <div class="character-image" :style="{ backgroundImage: 'url(' + character.thumbnail.path + '/portrait_fantastic.' + character.thumbnail.extension + ')' }"></div>
          <div class="character-name">{{ character.name }}</div>
        </div>
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
          console.log(this)
        const response = await this.$axios.$get('characters',{params:{
          apikey: 'ead4747ffb208c5281361a1be8e8edcd',
          
        }})       
         
        
        this.characters = response.data.results
        
    }
  }
  </script>
  
  <style scoped>
  .characters-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    background-color: #000;
    color: #fff;
    overflow: hidden;
    position: relative;
  }
  
  .characters-list {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
    margin-top: 50px;
    position: relative;
  }
  
  .character-card {
    flex: 0 0 auto;
    margin: 20px;
    width: 300px;
    height: 400px;
    position: relative;
    cursor: pointer;
    transition: transform 0.5s;
    z-index: 1;
  }
  
  .character-image {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    z-index: -1;
    transition: transform 0.5s;
  }
  
  .character-name {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    padding: 10px;
    background-color: rgba(0, 0, 0, 0.5);
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    z-index: 1;
  }
  
  .character-card:hover {
    transform: scale(1.1);
  }
  
  .character-card:hover .character-image {
    transform: translateX(-10px);
  }
  </style>