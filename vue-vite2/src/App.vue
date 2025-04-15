<template>
  <div>
    <h1>Las mejores Películas de la historia</h1>
    <div class="contenedor-peliculas">
      <CardComponent
      v-for="pelicula in peliculas"
      :key="pelicula.id"
      :movie="pelicula"
      @actualizar_likes="EventUpdateLikes"
/>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'; //Algunas cosas, que no me salian fueron hechas con la IA
import CardComponent from './components/CardComponent.vue'; 
import DatosPeliculas from '../src/resource/Peliculas'; 
import type { Pelicula } from './interfaces/Pelicula';


const peliculas = ref<Pelicula[]>(DatosPeliculas);

const EventUpdateLikes = (datosDelLike: { movieId: number; likes: boolean }) => {

  peliculas.value = peliculas.value.map((pelicula) => {
    if (pelicula.id === datosDelLike.movieId) {
      return { ...pelicula, likes: datosDelLike.likes ? pelicula.likes + 1 : pelicula.likes - 1 };
    }
    return pelicula;
  });
};


</script>

<style scoped>
.contenedor-peliculas {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around; 
  gap: 20px; 
}
</style>