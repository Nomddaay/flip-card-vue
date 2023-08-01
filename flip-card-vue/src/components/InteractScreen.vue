<template>
   <div class="screen">
    <h1>Interact Component</h1>
   </div>
   <card-flip 
    v-for="(card, index) in cardsContext" 
    :key="index" 
    :imgBackFaceUrl="`images/${card}.png`"
    :card="card"
    @onFlip="checkRule($event)"
    />
</template>

<script>
import { ref } from "vue";
import CardFlip from './Card.vue';

export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  }, 
  setup(props) {
    const rules = ref([]);
    
    const checkRule = (card) => {
      console.log(card);
    } 

    return {
      rules,
      checkRule,
    };
  },
  
  components: {
    CardFlip,
  },
}
</script>
