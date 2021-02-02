<template>
  <div class="home">
    <div class="home__main">
      <img
        class="img-boy"
        src="../assets/front-coin.png"/>
      <Coin
        :isActive="isActive"
        :state="state"
        class="home__coin"
      />
    </div>
    <div class="home__main">
      <div
       class="home__buttons"
       v-if="!isActive"
      >
        <button
          @click="flip('heads')"
          class="home__btn"
        >
         heads
        </button>
        <button
          @click="flip('tails')"
          class="home__btn"
        >
         tails
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Coin from '../components/Coin.vue'

export default {
  name: 'Home',
  components: {
    Coin
  },
  data () {
    return {
      isActive: false,
      state: ''
    }
  },
  methods: {
    flipping () {
      setTimeout(() => {
        this.isActive = false
        this.state = ''
      }, 4000)
    },
    flip (value) {
      this.isActive = !this.isActive
      this.state = value
      this.flipping()
    }
  }
}
</script>
<style lang="scss" scoped>

.img-boy {
  height: 130vh;
  position: absolute;
  left: 5%;
  top: -25%;
}
.home {
  height: 150vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;

  &__main {
    position: relative;
  }

  // &__coin {
  //   position: absolute;
  //   z-index: 1;
  // }

  &__btn {
    padding: 0.35em 1.2em;
    border: 0.1em solid #ffffff;
    margin: 0 0.3em 0.3em 0;
    border-radius: 0.12em;
    font-family: 'Roboto', sans-serif;
    font-weight: 300;
    color: #1b1818;
    text-align: center;
    transition: all 0.2s;
  }
  &__buttons {
    display: flex;
    width: 100%;
    justify-content: space-around;
  }
}
</style>
