<template>
  <div class="track-info">
    <h2>{{ track.title }}</h2>
    <p>{{ track.artist }}</p>
    <!-- Aquí está el ícono de la nota musical -->
    <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#5f6368"><path d="M500-360q42 0 71-29t29-71v-220h120v-80H560v220q-13-10-28-15t-32-5q-42 0-71 29t-29 71q0 42 29 71t71 29ZM320-240q-33 0-56.5-23.5T240-320v-480q0-33 23.5-56.5T320-880h480q33 0 56.5 23.5T880-800v480q0 33-23.5 56.5T800-240H320Zm0-80h480v-480H320v480ZM160-80q-33 0-56.5-23.5T80-160v-560h80v560h560v80H160Zm160-720v480-480Z"/></svg>
  </div>
</template>

  
  <script>
  export default {
    name: "TrackInfo",
    props: {
      track: Object,
    },
  };
  </script>
  
  <style scoped>
  .track-info {
    font-size: 14px; /* Ajusta el tamaño de la fuente */
      /* Ajusta el espacio interno */
    margin: 0 auto;  /* Centra el contenedor si es necesario */
    max-width: 90%;
  height:10%;
  display: flex;
  flex-direction: column;
  /* Ajusta a la altura que necesites, puede ser automática */
  margin-top: 80px;
  margin-bottom: 10vmax;

;
    justify-content: center;
    gap: 20px;
    padding: 1em;
    background-color: #121212;
    border: 4px solid #ff0055;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(255, 0, 85, 0.5);
    width: 100%;
    
    
    
}

@media (max-width: 768px) {
    .trackinfo, .audio-player {
        margin-bottom: 5vw;
        margin-top: 5vw;
    }
}

@media (max-width: 480px) {
    .trackinfo, .audio-player {
        margin-bottom: 80vw;
        margin-top: 80vw;
    }
}


.track-info h2, .track-info p {
  margin: 0;
  color: #ff0055;
  height: 40px;
}

.track-info svg {
  fill: #ff0055;  /* Cambia el color de la nota musical */
  margin-top: 10px; 
  width: 40px;
  height: 40px;
  } /* Ajustamos el espacio entre el texto y el ícono */
  .track-info {
  height: 50%; /* Puedes hacer que ocupe solo la mitad del alto del contenedor */
}
</style>