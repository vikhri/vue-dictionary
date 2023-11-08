<template>
  <form class="search-form container" :class="{ 'is-empty': isEmpty }" @submit.prevent="submitSearch(getData)">
      <input class="search-form__input" type="text" ref="SearchInput" placeholder="Enter a word in English">
    <button class="search-form__button" >
      <svg class="search-form__icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30">
        <path d="M 13 3 C 7.4889971 3 3 7.4889971 3 13 C 3 18.511003 7.4889971 23 13 23 C 15.396508 23 17.597385 22.148986 19.322266 20.736328 L 25.292969 26.707031 A 1.0001 1.0001 0 1 0 26.707031 25.292969 L 20.736328 19.322266 C 22.148986 17.597385 23 15.396508 23 13 C 23 7.4889971 18.511003 3 13 3 z M 13 5 C 17.430123 5 21 8.5698774 21 13 C 21 17.430123 17.430123 21 13 21 C 8.5698774 21 5 17.430123 5 13 C 5 8.5698774 8.5698774 5 13 5 z"></path>
      </svg>
    </button>
  </form>
  <p v-if="isEmpty" class="error">Enter a word</p>
</template>

<script>
import {inject} from "vue";

export default {
  data() {
    return {
      isEmpty: false,
    }
  },
  inject: ["getData"],
  methods: {
  submitSearch(getDataFunc) {

    // Валидация пустого поля
    if (this.$refs.SearchInput.value === '') {
      this.isEmpty = true

      return;
    }

    else {
      this.isEmpty = false;
      const SearchInput = this.$refs.SearchInput.value;
      console.log(SearchInput);

      getDataFunc(SearchInput);

      this.$refs.SearchInput.value = '';
    }

  }
  },
}

</script>

<style scoped>
  .search-form {
    width: 100%;
    max-width: 500px;
    height: 2em;
    display: flex;
    margin: 0 auto;
    border: 1px solid black;
    border-radius: 4px;
    transition: border-color 500ms;
  }

  .search-form__input {
    display: flex;
    align-items: center;
    flex-grow: 1;
    width: 100%;
    height: 100%;
    background-color: transparent;
    color: #1a1a1a;
    padding: 5px;
    padding-left: 10px;
    text-align: left;
  }

  .search-form__input::placeholder {
    color: lightgray;
    font-size: 1em;
  }

  .search-form__button {
    width: 2em;
    height: 2em;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
    background-color: transparent;

  }

  .search-form__icon {
    width: 20px;
    height: 20px;
    fill: #1a1a1a;
  }

  .is-empty {
    border-color: red;
  }

  .error {
    color: red;
    font-size: 0.7em;
  }

</style>
