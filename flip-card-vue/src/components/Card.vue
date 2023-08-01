  <template>
    <div class="card">
      <div 
        class="card__inner" @click="onToggleFlipCard" 
        :class="{ 'is-flipped': isFlipped }"
      >
        <div class="card__face card__face--front">
          <div class="card__content"></div>
        </div> 
        <div class="card__face card__face--back">
          <div 
            class="card__content" 
            :style="{ backgroundImage: `url(src/assets/${imgBackFaceUrl})` }"
          ></div>
        </div>
      </div>
    </div>
  </template>

  <script>
  import { ref, defineEmits } from 'vue'; // Import ref from Vue 3's Composition API

  export default {
    props: {
      card: {
        validator: (value) =>
        Array.isArray(value) || typeof value === 'string' || typeof value === 'number' || value instanceof Object,
      },

      imgBackFaceUrl: {
        type: String,
        required: true,
      },

      rules: {
        type: Array,
      },
    },
    setup(props) {
      const isFlipped = ref(false); // Use ref from Composition API
      

      const onToggleFlipCard = () => {
        isFlipped.value = !isFlipped.value;
        if (isFlipped.value) {
          
        }
      };

      return {
        isFlipped,
        onToggleFlipCard,
      };
    }
  }
  </script>

  <style lang="css" scoped>
    .card {
      display: inline-block;
      margin-right: 1rem;
      margin-bottom: 1rem;
      width: 90px;
      height: 120px;
    }

    .card__inner {
      width: 100%;
      height: 100%;
      transition: transform 1s;
      transform-style: preserve-3d;
      cursor: pointer;
      position: relative;
    }

    .card__inner.is-flipped {
      transform: rotateY(-180deg);
    }

    .card__face {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      overflow: hidden;
      border-radius: 1rem;
      padding: 1rem;
      box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
    }

    .card__face--front .card__content {
      background: url('@/assets/images/icon_back.png') no-repeat center center;
      background-size: 40px 40px;
      height: 100%;
    }

    .card__face--back {
      background-color: var(--light);
      transform: rotateY(-180deg);
    }

    .card__face--back .card__content {
      background-size: contain;
      background-position: center center;
      background-repeat: no-repeat;
      height: 100%;
      width: 100%;
    }
  </style>
