<template>
  <div id="game">
    <Overview/>
    <Upgrades/>
  </div>
</template>

<script>
import Overview from './components/Overview.vue';
import Upgrades from './components/Upgrades.vue';

export default {
  name: 'app',
  components: {
    Overview,
    Upgrades
  },
  methods: {
    coding() {
      this.$store.commit('incrementBytes', this.$store.state.bpk)
    },
    loop () {
      // GAME LOOP
      this.levelManager();
      requestAnimationFrame(this.loop)
    },
    levelManager () {
      if (this.$store.getters.bytesUntilLevelUp <= 0){
        this.$store.commit('levelUp');
      }
    }
  },
  created () {
    this.loop();
    document.addEventListener('keydown', this.coding);
  },
  unmounted () {
    document.addEventListener('keydown', this.coding);
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'montserrat', sans-serif;
  }
</style>
