<template>
  <form class="autocomplete">
    <label class="autocomplete__result" for="search">
      You selected:
      <span class="autocomplete__bold" v-if="selectedCountry">{{
        selectedCountry
      }}</span>
    </label>
    <input
      class="autocomplete__input"
      type="text"
      id="search"
      placeholder="Type here.."
      v-model="searchTerm"
      autocomplete="off"
    />

    <ul class="autocomplete__list" v-if="searchCountries.length">
      <li
        class="autocomplete__item"
        v-for="country in searchCountries"
        :key="country.name"
        @click="selectCountry(country.name)"
        @keyup.enter="selectCountry(country.name)"
      >
        {{ country.name }}
      </li>
    </ul>
  </form>
</template>

<script>
import { ref, computed } from "vue";
import countries from "@/data/countries.json";

export default {
  name: "InputSearch",
  setup() {
    let searchTerm = ref("");
    const searchCountries = computed(() => {
      if (searchTerm.value === "") {
        return [];
      }
      return countries.filter((country) => {
        if (
          country.name.toLowerCase().includes(searchTerm.value.toLowerCase())
        ) {
          return country;
        }
      });
    });
    const selectCountry = (country) => {
      selectedCountry.value = country;
      searchTerm.value = "";
    };
    let selectedCountry = ref("");
    return {
      countries,
      searchTerm,
      searchCountries,
      selectCountry,
      selectedCountry,
    };
  },
};
</script>

<style lang="scss">
.autocomplete {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  max-width: 300px;

  &__label {
    margin-bottom: 10px;
    border-radius: 8px;
    font-weight: 700;
  }

  &__input {
    padding: 10px 5px;
    border: 1px solid gray;
    border-radius: 3px;
    margin-bottom: 10px;
    &:focus {
      border: 1px solid red;
    }
  }

  &__list {
    border: 1px solid gray;
    border-radius: 3px;
    padding: 5px 5px 0 5px;
    max-height: 500px;
    overflow: auto;
  }

  &__item {
    margin-bottom: 5px;
    &:hover {
      color: red;
    }
    &:active {
      color: red;
    }
  }

  &__result {
    margin-bottom: 10px;
  }

  &__bold {
    font-weight: 700;
    color: red;
  }
}
</style>
