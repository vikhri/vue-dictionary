<template>
  <h1>VUE Dictionary</h1>
  <InputField></InputField>
  <LoadingBar v-if="isLoading"></LoadingBar>
  <p class="errorMessage" v-if="errorMessage">{{ errorMessage }}</p>
  <div v-else>
    <PronounceBlock :word="MeaningData.word" :trans="MeaningData.trans" :audio="MeaningData.audio"></PronounceBlock>
    <MeaningBlock :meanings="MeaningData.meanings"></MeaningBlock>
  </div>
</template>

<script>

import InputField from "./components/InputField.vue";
import LoadingBar from "./components/LoadingBar.vue"
import {defineComponent} from "vue";
import PronounceBlock from "./components/PronounceBlock.vue"
import MeaningBlock from  "./components/MeaningBlock.vue"

export default defineComponent({
  components: {MeaningBlock, PronounceBlock, InputField, LoadingBar},
  data() {
    return {
      MeaningData: {
        word: '',
        trans: '',
        audio: '',
        meanings: [],
      },
      isLoading: false,
      errorMessage: null,
    }
  },
  provide() {
    return {
      getData: this.getData,
    }
  },
  // emits: ["meaningRequest"],
  methods: {
    async getData(word) {
      this.isLoading = true;
      this.errorMessage = null;

      try {
        const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`);

        if (response.ok) {
          const data = await response.json();
          if (data) {
            const newData = data[0];
            this.isLoading = false;

            this.MeaningData.word = newData.word;
            this.MeaningData.trans = newData.phonetic || newData.phonetics.find(item => item.text).text;
            this.MeaningData.meanings = newData.meanings;
            this.MeaningData.audio = newData.phonetics.find(item => item.audio !== '').audio;
          }
        } else if (response.status === 404) {
          this.isLoading = false;
          this.errorMessage = 'Not found';
        } else {
          throw new Error('Failed to fetch data');
        }
      }
      catch (error) {
        this.isLoading = false;
        this.errorMessage = 'Fail to fetch data. Try again later';
      }
    }
  }

})



</script>



<style scoped>
h1 {
  font-size: 3em;
  font-weight: 700;
  color: #a00078;
  padding: 0 20px 30px;
}

p {
  color: #1a1a1a;
}

.errorMessage {
  padding: 30px;
  color: #0076bb;
}

</style>
