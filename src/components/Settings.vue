<template>
    <div class="settings">
      <button @click="changeVolume(-0.1)" :disabled="!audio">
        <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M12 3v10.55a4.5 4.5 0 1 0 2 0V5h5V3h-7z"/></svg>
        <!-- Bajar volumen -->
      </button>
  
      <span v-if="audio">{{ Math.round(volume * 100) }}%</span>
      <span v-else>Cargando...</span> <!-- Mensaje si el audio aún no está disponible -->
  
      <button @click="changeVolume(0.1)" :disabled="!audio">
        <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M12 3v10.55a4.5 4.5 0 1 0 2 0V5h5V3h-7z"/></svg>
        <!-- Subir volumen -->
      </button>
    </div>
  </template>
  
  <script>
  import { defineProps, ref, watch } from "vue";
  
  export default {
    props: {
      audio: Object, // Recibe el objeto Howl desde AudioPlayer.vue
    },
    setup(props) {
      const volume = ref(0.5); // Volumen inicial
  
      // Observa cuando 'props.audio' esté disponible
      watch(() => props.audio, (newAudio) => {
        if (newAudio) {
            volume.value = newAudio.volume(); // Ajustar volumen inicial
        }
      });
  
      const changeVolume = (amount) => {
        if (!props.audio) return; // Si no hay audio, salir
        let newVolume = props.audio.volume() + amount;
        if (newVolume > 1) newVolume = 1;
        if (newVolume < 0) newVolume = 0;
        props.audio.volume(newVolume); // Cambia el volumen real
        volume.value = newVolume; 

        console.log("Nuevo volumen:", props.audio.volume());
      // Actualiza la UI
      };
  
      return { volume, changeVolume };
    },
  };
  </script>
  
  <style scoped>

.settings {
  display: flex;              /* Usamos flexbox */
  justify-content: center;    /* Centra los botones en el contenedor */
  gap: 20px;                  /* Espacio entre los botones */
  padding: 10px;              /* Espaciado alrededor de los botones */
  flex-wrap: nowrap;          /* Evita que los botones se acomoden en columnas si hay poco espacio */
}


.settings button {
  background: black;          /* Fondo negro */
  color: #ff0055;                /* Color del texto (o ícono) rosado */
  border: 2px solid #ff0055;     /* Borde rosado */
  padding: 10px 20px;         /* Ajusta el padding para el tamaño del botón */
  border-radius: 8px;         /* Bordes redondeados */
  font-size: 16px;            /* Tamaño de la fuente */
  cursor: pointer;           /* Cambia el cursor al pasar sobre el botón */
  display: flex;              /* Para que los íconos estén alineados */
  align-items: center;        /* Alineación de los íconos */
  justify-content: center;    /* Centra el contenido dentro del botón */
  transition: background-color 0.3s, color 0.3s;
  gap: 20px;
 /* Para animar el cambio de color */
}

.settings button:hover {
  background: #ff0055;          /* Fondo rosado cuando pasas el ratón */
  color: black;              /* Texto negro cuando pasas el ratón */
}

.settings svg {
  margin-right: 10px;         /* Espacio entre el ícono y el texto */
  fill: #ff0055;                 /* El color del ícono será rosado */
  width: 20px;                /* Ajusta el tamaño del ícono */
  height: 20px;               /* Ajusta el tamaño del ícono */
}
</style>
  
  