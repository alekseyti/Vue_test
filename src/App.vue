<template>
  <v-app>
    

    <v-main>
      <datePickers/>

    </v-main>
  </v-app>
</template>

<script>
import datePickers from './components/datePickers';

export default {
  name: 'App',

  components: {
    datePickers,
  },

  data: () => ({
    //
  }),
};
</script>
