<template>
  <form class="autocomplete">
    <label class="autocomplete__label" for="search"> Country: </label>
    <input
      class="autocomplete__input"
      type="text"
      id="search"
      placeholder="Type here.."
      v-model="searchTerm"
      autocomplete="off"
      list="country"
    />

    <datalist v-if="searchCountries.length" id="country">
      <option
        v-for="country in searchCountries"
        :key="country.name"
        @click="selectCountry(country.name)"
        @keyup.enter="selectCountry(country.name)"
        :value="country.name"
      ></option>
    </datalist>
    <input type="reset" value="clear" />
  </form>
</template>

<script>
import { ref, computed } from "vue";
import countries from "@/data/countries.json";

export default {
  name: "InputSearch",
  methods: {},
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
    const clearInput = (country) => {
      selectedCountry.value = country;
      country = "";
    };
    let selectedCountry = ref("");
    return {
      countries,
      searchTerm,
      searchCountries,
      selectCountry,
      selectedCountry,
      clearInput,
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
}
</style>
