<template>
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
</template>

<script>

export default {
  components: {},
  data () {
    const dateTime = new Date();
    const month = dateTime.getUTCMonth();
    return {
      dateTime,
      month,
    }
  },
  methods: {
    handleClockTimeChange ({ dateTime, isInTimeWindow }) {
      // only set value if it's changed
      if (this.isInTimeWindow !== isInTimeWindow) {
        this.isInTimeWindow = isInTimeWindow
        this.dateTime = dateTime
        // console.log('this.isInTimeWindow', this.isInTimeWindow)
        // console.log('this.dateTime', this.dateTime)
      }
    }
  }
}
</script>

<style scoped>
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
