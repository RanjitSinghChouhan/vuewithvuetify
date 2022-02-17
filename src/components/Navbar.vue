<template>
  <v-nav class="d-flex justify-center">
    <v-app-bar app class="text-uppercase grey">
      <v-toolbar-title>
        <span>MyList</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn color="pink">
        <span>Sign Out</span>
      </v-btn>
    </v-app-bar>
  </v-nav>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";

Options({});
export default class Navbar extends Vue {}
</script>

<style scoped>
</style>