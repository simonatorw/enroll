<template>
  <v-app>
    <v-toolbar app class="header">
      <v-toolbar-title class="">
        <span>AbleTo</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <Step/>
    </v-content>
  </v-app>
</template>

<script>
import Step from './components/Step'

export default {
  name: 'App',
  components: {
    Step
  },
  data () {
    return {
      //
    }
  }
}
</script>

<style>
  .theme--light.application {
    background-color: #f9f6f4;
  }
  .theme--light.header {
    background-color: white;
  }
</style>
