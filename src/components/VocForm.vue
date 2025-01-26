<template>
  <br>
  <div class="vocab-box-titre" >
    <div class="vocab-column">
      <h2>Prononciation</h2>
    </div>
    <div class="vocab-column">
      <h2>Albanais</h2>
    </div><div class="vocab-column">
      <h2>Français</h2>
    </div>
  </div>
      <br>
  <div class="vocab-page">
    <div v-for="(item, index) in vocabList" :key="index" class="vocab-box" >
      <div class="vocab-column">
        <p><button class="audio-button" @click="playAudio(item.audio)">
            <i class="bi bi-volume-up-fill"></i>
          </button>
          {{ item.prononciation }}

        </p>
      </div>
      <div class="vocab-column">
        <p>{{ item.albanais }}</p>
      </div>
      <div class="vocab-column">
        <p>{{ item.francais }}</p>
      </div>
    </div>
  </div>
  <br><br><br><br>
</template>

<script setup>
import { ref } from 'vue';

const vocabList = ref([
  {
    francais: "SALUT À TOUS",
    prononciation: "SALY A TUS",
    albanais: "KOH TE GJAT SJEMI PA",
    audio : ""
  },
  {
    francais: "ÇA FAISAIT LONGTEMPS",
    prononciation: "SA FÝZE LONTA",
    albanais: "KOH TE GJAT SJEMI PA",
  },
  {
    francais: "JE SUIS HEUREUX DE TE RENCONTRER",
    prononciation: "ZHÝ SFI ZÝRRÝ DÝ TÝ RRAKONTRE",
    albanais: "GEZOHEM TE JU TAKOJ",
    audio : ""
  },
  {
    francais: "À PLUS TARD",
    prononciation: "A PLY TARR",
    albanais: "SHIHEMI ME VON",
    audio : ""
  },
  {
    francais: "A BIENTÔT",
    prononciation: "À BJENTO",
    albanais: "SHIHEMI SE SHPEJTI",
    audio: "audios/a_bientot.m4a"
  },
  {
    francais: "AU REVOIR",
    prononciation: "ORRÝVARR",
    albanais: "MIR U PAFSHIM",
    audio : ""
  },
  {
    francais: "À DEMAIN",
    prononciation: "À DEMAINA DÝMË",
    albanais: "SHIMEM NESTER",
    audio : ""
  },
  {
    francais: "JE T’AIME BIEN",
    prononciation: "ZHÝ TEM BJË",
    albanais: "ME PELQEN TI",
    audio : ""
  },
  {
    prononciationfrancais: "TY E TRO DROL",
    francais: "TU ES TROP DRÔLE",
    albanais: "JU JENI I KENDSHEM",
    audio : ""
  },

  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
  {
    prononciationfrancais: "",
    francais: "",
    albanais: "",
    audio : ""
  },
]);


function playAudio(audioFile) {
  const audio = new Audio(audioFile);
  audio.play();
}

</script>

<style scoped>
.vocab-page {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.vocab-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgb(194, 226, 254);
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  width: 100%;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.vocab-box-titre{
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgb(48, 157, 252);
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  width: 100%;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.vocab-column {
  flex: 1;
  text-align: center;
}

.vocab-column h2 {
  font-size: 20px;
  margin-bottom: 8px;
  text-align: left;
}

.vocab-column p {
  font-size: 17px;

  margin: 0;
  text-align: left;
}


.audio-button {
  background: none;
  border: none;
  font-size: 16px;
  margin-left: 8px;
  cursor: pointer;
  color: black;
}

.audio-button:hover {
  color: #0056b3;
}
</style>
