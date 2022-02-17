<template>
  <v-app>
    <Navbar />
    <br />
    <br />
    <Fetch />
  </v-app>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Navbar from "./components/Navbar.vue";
import Fetch from "./components/Fetch.vue";
@Options({
  components: {
    Fetch,
    Navbar,
  },
})
export default class App extends Vue {}
</script>
 
<style scoped>
</style>