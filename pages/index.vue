<template>
  <main class="page" :style="{'background-image': 'url(45-degree-fabric-light.png)'}">
    <div class="container">
      <section class="title-wrapper">
        <h1 class="title">
          Flowers For {{name}}
        </h1>
      </section>
      <section class="flower-wrapper">
        <img class="flower-image" :src="month + '-flowers.jpg'">
      </section>
      <section class="bee-grid">
        <AnimatedCell
          v-for="index in totalBees"
          :key="index + rainDirection"
          :delay-max="delayMax"
          :delay-min="delayMin"
          :duration-max="durationMax"
          :duration-min="durationMin"
          :horizontal-max="horizontalMax"
          :horizontal-min="horizontalMin"
          :rain-direction="rainDirection"
          :size-max="sizeMax"
          :size-min="sizeMin"
          :vertical-max="verticalMax"
          :vertical-min="verticalMin"
        >🐝</AnimatedCell>
      </section>
    </div>
  </main>
</template>

<script>
import AnimatedCell from '~/components/animated-cell.vue';
const NAME_DEFAULT = 'Ur Mum';

export default {
  components: {
    AnimatedCell,
  },
  head () {
    return {
      title: '🌹🐝',
    }
  },
  data () {
    return {
      name: NAME_DEFAULT,
      month: '',
      flowerz: ['🌹', '🌸', '💐', '🌺', '🌷', '🌻', '🌼', '💮', '🪷'],
      delayMax: 0,
      delayMin: 0,
      durationMax: 10,
      durationMin: 15,
      horizontalMax: 100,
      horizontalMin: 0,
      rainDirection: 2,
      sizeMax: 2,
      sizeMin: 0.5,
      totalBees: 10,
      verticalMax: 100,
      verticalMin: 0,
    }
  },
  methods: {
    getMonth() {
      const monthQuery = this.$route.query.month;
      // handle null and undefined cases
      const hasMonthQuery = Boolean(monthQuery !== null && monthQuery !== undefined);
      // convert string to number if value is not undefined or null
      const monthQueryValue = hasMonthQuery ? Number(monthQuery) : undefined;
      // determine if value is a number that is between 0 and 11, inclusive
      const isValidMonthOverride = Boolean(!isNaN(monthQueryValue) && monthQueryValue <=11 && monthQueryValue >= 0);
      const dateTime = new Date();
      // if the query value is valid, use it, otherwise use the current datetime
      const month = isValidMonthOverride ? monthQueryValue : dateTime.getUTCMonth();

      this.month = month;
    },
    setTitle() {
      var interval = setInterval(() => {
        const flower = this.flowerz.sort((a, b) => 0.5 - Math.random())[0];
        document.title = `${flower}🐝`;
      }, 5000);
    },
    getName() {
      const nameQuery = this.$route.query.name;
      const name =  nameQuery ? nameQuery : NAME_DEFAULT

      this.name = name;
    }
  },
  mounted() {
    this.getName();
    this.getMonth();
    this.setTitle();
  }
}
</script>

<style scoped>
.page {
  height: 100%;
  width: 100%;
  background-repeat: repeat;
}

.bee-grid {
  position: absolute;
  display: flex;
  flex-wrap: wrap;
  height: 100%;
  width: 100%;
  overflow: hidden;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 1rem;
  max-width: 40rem;
}

.title-wrapper {
  height: 100%;
  width: 100%;
  justify-content: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 2rem;
  color: #35495e;
  letter-spacing: 1px;
}

.flower-wrapper {
  width: 100%;
  height: auto;
}

.flower-image {
  width: 100%;
  height: auto;
}
</style>
