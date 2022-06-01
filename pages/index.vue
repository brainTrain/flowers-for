<template>
  <main class="page" :style="{'background-image': 'url(45-degree-fabric-light.png)'}">
    <div class="container">
      <section class="title-wrapper">
        <h1 class="title">
          Flowers For Katy
        </h1>
      </section>
      <section class="flower-wrapper">
        <img class="flower-image" :src="month + '-flowers.jpg'">
      </section>
    </div>
  </main>
</template>

<script>

export default {
  components: {},
  head () {
    return {
      title: '🌹',
    }
  },
  data () {
    return {
      month: '',
      flowerz: ['🌹', '🌸', '💐', '🌺', '🌷', '🌻', '🌼', '💮', '🪷'],
    }
  },
  methods: {
    getMonth() {
      const dateTime = new Date();
      const month = dateTime.getUTCMonth();
      this.month = month;
    },
    setTitle() {
      var interval = setInterval(() => {
        const flower = this.flowerz.sort((a, b) => 0.5 - Math.random())[0];
        document.title = flower;
      }, 5000);
    }
  },
  mounted() {
    this.getMonth();
    this.setTitle();
  }
}
</script>

<style>
</style>

<style scoped>
.page {
  height: 100%;
  width: 100%;
  background-repeat: repeat;
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
