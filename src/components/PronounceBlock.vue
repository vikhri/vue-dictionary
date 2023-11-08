<template>
  <div class="pronounce container" v-if="word != ''">
    <div class="pronounce__text">
      <p class="pronounce__word">{{ word }}</p>
      <p class="pronounce__trans">{{ trans }}</p>
    </div>
    <div class="pronounce__audio">
      <audio id="audio" :src="audio"> </audio>
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
</template>

<script>
export default {
  name: "PronounceBlock.vue",
  props: {
    word: String,
    trans: String,
    audio: String,
  },
  methods: {
    playAudio() {
      document.getElementById("audio").play();
      console.log(document.getElementById("audio"))
    },
  }
}

</script>

<style scoped>

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
  cursor: pointer;
}
.pronounce__play-btn:hover {
  opacity: 80%;
}
.pronounce__play-btn:active {
  background-color: #0076bb;
}
</style>