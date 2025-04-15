<template>
  <div class="card-content">
    <h3>{{ movie.titulo }}</h3>
    <p>Año: {{ movie.anio }}</p>
    <p>Género: {{ movie.genero }}</p>
    <p>Director: {{ movie.director }}</p>
    <div>
  <img v-if="movie.portada"
       :src="movie.portada"
       :alt="movie.titulo"
  />
  <div v-else>Portada no disponible</div>
    <p>Likes: {{ movie.likes }}</p>
    <button @click="CountLikes" :style="`background-color: ${likes ? 'red' : 'green'}`">
    <Icon v-if="likes"  icon="ic:baseline-clear" width="24" height="24"/>
    <Icon v-else icon="ic:baseline-check" width="24" height="24" />

      {{ likes ? 'Quitar Like ' : 'Dar Like' }}
      
    </button>
  </div>
</div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, ref} from 'vue';
import type { Pelicula } from '../interfaces/Pelicula';
import { Icon } from '@iconify/vue';

const props = defineProps<{
movie: Pelicula;
}>();

const emit = defineEmits(['actualizar_likes']); 

const likes = ref(false); 

const CountLikes = () => {
likes.value = !likes.value;

emit('actualizar_likes', { movieId: props.movie.id, likes: likes.value });
};
</script>

<style scoped>
button {
background-color: #2135e4;
color: whitesmoke;
border: solid 2.5px black;
margin-bottom: 10px;
}

img {  
width: 400px;
height: 600px;
}

.card-content {
  border: 2.5px solid black;
  background-color: rgb(61, 23, 61);
  margin-bottom: 20px;
  border-radius: 10px;
  width: calc(25% - 10px);
}
</style>