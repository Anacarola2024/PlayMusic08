
<template>
  <div class="player-controls">
    <!-- Botón Anterior (Doble Flecha) -->
    <button @click="$emit('prev')">
      <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24">
        <path d="M8 4l-5 5h3v6h4V9h3L8 4zM16 20l5-5h-3v-6h-4v5h-3l5 5z"/>
      </svg>
      Anterior
    </button>

    <!-- Botón Reproducir/Pausar -->
    <button @click="$emit('toggle-play')">
      <!-- Mostrar ícono de reproducción o pausa según el estado -->
      <svg v-if="!isPlaying" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24">
        <path d="M8 5v14l11-7z"/>
      </svg>
      <svg v-else xmlns="http://www.w3.org/2000/svg" fill="pink" width="20" height="20" viewBox="0 0 24 24">
        <path d="M8 5v14l11-7z"/>
      </svg>
      {{ isPlaying ? 'Pausar' : 'Reproducir' }}
    </button>

    <!-- Botón Siguiente (Doble Flecha) -->
    <button @click="$emit('next')">
      <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24">
        <path d="M8 4l-5 5h3v6h4V9h3L8 4zM16 20l5-5h-3v-6h-4v5h-3l5 5z"/>
      </svg>
      Siguiente
    </button>
  </div>
</template>

<script>
export default {
  name: "PlayerControls",
  props: {
    isPlaying: Boolean,
  },
};
</script>

<style scoped>
.material-icons {
  font-family: 'Material Icons';
  font-size: 24px;
}

.player-controls {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 15px;
  background-color: #121212;
  border: 4px solid #ff0055;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(255, 0, 85, 0.5);
}

button {
  background-color: #ff0055;
  color: white;
  border: none;
  padding: 15px 25px;
  font-size: 18px;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

button:hover {
  transform: scale(1.1);
  box-shadow: 0 0 15px rgba(255, 0, 85, 0.7);
}
</style>
