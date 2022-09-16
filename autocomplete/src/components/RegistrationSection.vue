<template>
  <section class="registration">
    <InputSearch />
  </section>
</template>

<script>
import InputSearch from "./InputSearch.vue";
export default {
  name: "RegistrationSection",
  components: {
    InputSearch,
  },
};
</script>

<style lang="scss">
.registration {
  max-width: 1390px;
  width: 100%;
  padding: 20px 15px;
  margin: 0 auto;
}
</style>
