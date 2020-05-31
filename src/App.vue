<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    </v-app-bar>

    <v-content>
      <Test/>
    </v-content>
  </v-app>
</template>

<script>
import Test from './components/Test';

export default {
  name: 'App',

  components: {
    Test,
  },

  data: () => ({
    //
  }),
};
</script>
