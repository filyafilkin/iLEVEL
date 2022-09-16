<template>
  <main>
    <RegistrationSection />
  </main>
</template>

<script>
import RegistrationSection from "./components/RegistrationSection.vue";
export default {
  name: "App",
  components: {
    RegistrationSection,
  },
};
</script>

<style lang="scss">
@import url("@/assets/reset.css");

#app {
  font-family: "Roboto", sans-serif;
  box-sizing: border-box;
}
</style>
