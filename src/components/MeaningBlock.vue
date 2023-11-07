<template>
  <div class="meaning container">
    <ul class="meaning__list" v-for="meaning in meanings">
      <li class="meaning__list-item">
        <div class="meaning__inner">
          <p class="meaning__type">
            {{ meaning.partOfSpeech }}
          </p>
          <div class="meaning__block">
            <h3 class="meaning__heading">Meaning</h3>
            <ul class="meaning__defs" v-for="def in meaning.definitions">
              <li class="meaning__text">
                {{ def.definition }}
              </li>
            </ul>
          </div>
          <div class="meaning__block" v-if="meaning.synonyms.length > 0">
            <h3 class="meaning__heading">Synonyms</h3>
            <p class="meaning__text">
              {{ meaning.synonyms.join(', ') }}
            </p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import {inject} from "vue";

export default {
  name: "MeaningBlock.vue",
  props: ["meanings"],
}

</script>

<style scoped>
.meaning {
  color: #1a1a1a;
  text-align: left;
}

.meaning__list-item {
  border-bottom: 1px solid lightgray;
  padding-block: 10px;
}

.meaning__type {
  color: #489DFF;
  font-weight: 700;
}

.meaning__heading {
  font-style: italic;
  color: lightgray;
}

.meaning__defs {
  list-style: circle;
  padding-left: 30px;
}

.meaning__text {
  color: #1a1a1a;
  font-size: 0.7em;
}

.meaning__inner {
  display: flex;
  flex-direction: column;
  row-gap: 10px;
}
</style>