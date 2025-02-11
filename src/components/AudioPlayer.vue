<template>
    <div class="audio-player">
      <TrackInfo :track="currentTrack" />
      <PlayerControls :isPlaying="isPlaying" @toggle-play="togglePlay" @next="nextTrack" @prev="prevTrack" />
      <Settings :audio="audio" /> <!-- Pasamos el audio a Settings.vue -->
    </div>
  </template>
  
  <script>
  import { Howl } from "howler";
  import TrackInfo from "@/components/TrackInfo.vue";
  import PlayerControls from "@/components/PlayerControls.vue";
  import Settings from "@/components/Settings.vue"; // Importar el nuevo componente
  
  export default { //nombre del componente
    components: {
      TrackInfo,
      PlayerControls,
      Settings, // Registrar el componente Settings
    },
    data() {
      return {
        audio: null,
        isPlaying: false,
        currentTrackIndex: 0,
        tracks: [
          { title: " Cancion: Disco Party", artist: " Artista: Alexei Anisimov", url: "src/assets/Alexey_Anisimov_-_Disco_Party.mp3" },
         
          { title: " Cancion: Sound for you", artist: " Artista: Power Drive", url:  "src/assets/Power_Drive_-_SoundForYou.mp3" },
          { title: " Cancion: Ilya sound", artist: " Artista: Rock Game Trailer", url: "src/assets/Rock_Game_Trailer_-_IlyaSound.mp3" },
          { title: " Cancion: Roller Genoa",artist: " Artista: Safe And Warm in Hunter Arms", url: "src/assets/Safe_and_Warm_in_Hunter's_Arms_-_Roller_Genoa_(2).mp3" },
          { title: " Cancion:The Other Side", artist: "Artista: Sh Music", url: "src/assets/THE_OTHER_SIDE_-_SH_MUSIC_(lukhash).mp3" },
          { title: " Cancion:wire & flashing lights", artist: " Artista: Professor Kliq", url: "src/assets/Wire_&_Flashing_Lights_-_Professor_Kliq.mp3" },
        ],
        currentTrack: { title: "", artist: "", url: "" },
      };
    },
    methods: {
      playTrack() {
        if (this.audio) {
          this.audio.stop(); // Detener la pista anterior antes de reproducir la nueva
        }
  
        this.audio = new Howl({
          src: [this.currentTrack.url],
          html5: true, // Usar HTML5 para reproducir el audio en moviles
          volume: 1.0,// Volumen inicial
          onend: this.nextTrack, //cuando termnina la cancion pasa a la siguiente automaticamente
        });
  
        this.audio.play(); //Inicia la pista
        this.isPlaying = true; // Cambia el estado de reproducción a REPRODUCIENDO
      },
      togglePlay() {
        if (this.isPlaying) {
          this.audio.pause(); //si esta reproduciendo lo pausa
        } else {
          if (!this.audio) {
            this.playTrack(); //si no hay una cancion cargada , inicia la cancion
          } else {
            this.audio.play();// si ya existe simplemente la reanuda
          }
        }
        this.isPlaying = !this.isPlaying; // cambia el estado entre play y pause
      },
      nextTrack() {
        this.currentTrackIndex = (this.currentTrackIndex + 1) % this.tracks.length; //siguiente cancion (con loo)
        this.currentTrack = this.tracks[this.currentTrackIndex];// Actualiza la cancion
        this.playTrack();
      },
      prevTrack() {
        this.currentTrackIndex = (this.currentTrackIndex - 1 + this.tracks.length) % this.tracks.length;//canc
        this.currentTrack = this.tracks[this.currentTrackIndex];// Actualiza la cancion
        this.playTrack(); //reproduce la nueva cancion
      },
    },
    mounted() {
      this.currentTrack = this.tracks[this.currentTrackIndex]; //asigna la primera cancion cuando se carga el componente
    },
  };
  </script>
  
  <style scoped>
  .audio-player {
    min-height: 100vh;             /* Ocupa todo el alto de la ventana */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
    width: 100%;
    background-image: url("src/assets/marcela-laskoski-YrtFlrLo2DQ-unsplash(1).jpg");
    background-size: cover;    /* Asegura que la imagen cubra el contenedor */
    background-position: center;
    background-attachment: fixed; /* Fija la imagen en su lugar */
}
.volume-controls {
    position: absolute;         /* Posiciona los controles dentro del contenedor */
    bottom: 20px;               /* Ajusta la distancia desde la parte inferior */
    display: flex;
    justify-content: center;
    width: 100%;
}

@media (max-width: 768px) {
    .audio-player {
        background-attachment: scroll; /* Cambia a scroll en pantallas más pequeñas */
    }
}
.volume-controls {
        bottom: 10px;           /* Ajusta la distancia en pantallas pequeñas */
    }

@media (max-width: 480px) {
    .audio-player {
        min-height: 80vh;    /* Ajusta la altura en pantallas pequeñas para no sobrecargar */
    }
}


  </style>
  