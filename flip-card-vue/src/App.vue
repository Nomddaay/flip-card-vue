<script>
  import MainScreen from './components/MainScreen.vue';
  import InteractScreen from './components/InteractScreen.vue';

  import { shuffled } from './utils/array'

  export default {
    name: 'App',
    data() {
      return {
        settings: {
          totalOfBlocks: 0,
          cardsContext: [],
          startedAt: null,

        },
        statusMatch: "default",
      }
    },
    components: {
      MainScreen,
      InteractScreen,
    },
    methods: {
      onHandBeforeStart(config) {
        console.log("running", config);
        this.settings.totalOfBlocks = config.totalOfBlocks;

        const firstCards = Array.from(
          { length: this.settings.totalOfBlocks / 2 },
          (_, i) => i + 1,
        );
        const secondCards = [...firstCards];
        const cards = [...firstCards, ...secondCards];
        console.log(cards);
        this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
        this.settings.startedAt = new Date().getTime();

        this.statusMatch = "match";
      }
    }
  }
</script>

<template>
  <main-screen v-if="statusMatch === 'default'" @onStart="onHandBeforeStart($event)"/>
  <interact-screen 
    v-if="statusMatch === 'match'" 
    :cardsContext="settings.cardsContext"
  />
</template>


