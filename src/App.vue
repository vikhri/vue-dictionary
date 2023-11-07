<template>
  <InputField></InputField>
<!--  pron-->
  <div class="pronounce container" v-if="MeaningData.word != ''">
    <div class="pronounce__text">
      <p class="pronounce__word">{{MeaningData.word}}</p>
      <p class="pronounce__trans">{{MeaningData.trans}}</p>
    </div>
    <div class="pronounce__audio">
      <audio id="audio" :src="MeaningData.audio"> </audio>
      <button class="pronounce__play-btn" @click="playAudio">
        <svg
            width="24"
            height="24"
            viewBox="0 0 100 100"
            xmlns="http://www.w3.org/2000/svg"
        >
          <polygon points="30,20 30,80 80,50" fill="white" />
        </svg>
      </button>
      <audio class="pronounce__track"></audio>
    </div>
  </div>
<!--  pron-->
  <MeaningBlock :meanings="MeaningData.meanings"></MeaningBlock>
  <p></p>
</template>

<script>

import InputField from "./components/InputField.vue";
import {defineComponent} from "vue";
import PronounceBlock from "./components/PronounceBlock.vue"
import MeaningBlock from  "./components/MeaningBlock.vue"

export default defineComponent({
  components: {MeaningBlock, PronounceBlock, InputField},
  data() {
    return {
      MeaningData: {
        word: '',
        trans: '',
        audio: '',
        meanings: [],
      },
    }
  },
  provide() {
    return {
      getData: this.getData,
    }
  },
  // emits: ["meaningRequest"],
  methods: {
    getData(word) {

      fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
        .then((res) => res.json())
        .then((data) => {
          const newData = data[0];
          this.MeaningData.word = newData.word;
          this.MeaningData.trans = newData.phonetic;
          this.MeaningData.meanings = newData.meanings;
          this.MeaningData.audio = newData.phonetics.find(item => item.audio !== '').audio;

          console.log(newData);
        })

    },
    playAudio() {
      document.getElementById("audio").play();
      console.log(document.getElementById("audio"))
    }
  }

})



</script>



<style scoped>
p {
  color: #1a1a1a;
}


.pronounce {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding-block: 20px;
}

.pronounce__text {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  row-gap: 10px;
}
.pronounce__word {
  font-size: 2.5em;
  line-height: 1;
  font-weight: bold;
  color: #0076bb;
  text-transform: capitalize;
}
.pronounce__trans {
  font-size: 1em;
  font-weight: initial;
  color: #489DFF;
}
.pronounce__audio {
  display: flex;
  justify-content: flex-end;
}
.pronounce__play-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  background-color: #489DFF;
  color: white;
  border-radius: 50%;
}

</style>
