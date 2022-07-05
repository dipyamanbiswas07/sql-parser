<template>
  <v-app>
    <v-app-bar dense app color="primary" dark>
      <div class="d-flex align-center h1 title">SQL Parser</div>
    </v-app-bar>
    <v-main>
      <parser-container />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import ParserContainer from './components/ParserContainer.vue';

@Component({
  components: { ParserContainer },
})
export default class App extends Vue {}
</script>
<style>
html {
  overflow-y: auto !important;
}
</style>
