<template>
  <div
    class="cell"
    v-bind:style="styleObject"
  >
    <slot></slot>
  </div>
</template>

<script>
const randomNumber = (min, max) => (Math.random() * (max - min) + min);
const calculateDirection = (value) => (`${parseInt(value) * 100}vh`);

export default {
  props: {
    delayMax: Number,
    delayMin: Number,
    durationMax: Number,
    durationMin: Number,
    horizontalMax: Number,
    horizontalMin: Number,
    rainDirection: [Number, String],
    sizeMax: Number,
    sizeMin: Number,
    verticalMax: Number,
    verticalMin: Number,
  },
  data: function () {
    const {
      delayMax,
      delayMin,
      durationMax,
      durationMin,
      horizontalMax,
      horizontalMin,
      rainDirection,
      sizeMax,
      sizeMin,
      verticalMax,
      verticalMin,
    } = this;

    return {
      styleObject: {
        '--direction': calculateDirection(rainDirection),
        top: `${randomNumber(verticalMin, verticalMax)}%`,
        left: `${randomNumber(horizontalMin, horizontalMax)}%`,
        fontSize: `${randomNumber(sizeMin, sizeMax)}rem`,
        animationDuration: `${randomNumber(durationMin, durationMax)}s`,
        animationDelay: `${randomNumber(delayMin, delayMax)}s`
      }
    };
  },
  watch: {
    rainDirection: function (newValue, oldValue) {
      const newDirection = calculateDirection(newValue);
      const newStyle = {
        ...this.styleObject,
        '--direction': newDirection,
      };

      this.styleObject = newStyle;
    },
  },
}
</script>

<style>
:root {
  --direction: 200vh;
}
</style>

<style>
.cell {
  position: absolute;
  /*animation: fly linear infinite, hover ease-in-out infinite;*/
  animation: bee ease-in-out infinite;

  /* keyframe style initialization */
  transform: translate(0, 0) rotate(0deg);
}

@keyframes bee {
	0% {
		transform: translate(-50vw, 0) scaleX(-1);
	}
  49% {
		transform: translate(0, -3rem) scaleX(-1);
  }
	50% {
		transform: translate(0, -3rem) scaleX(1);
	}
  99% {
		transform: translate(-50vw, 0) scaleX(1);
  }
	100% {
		transform: translate(-50vw, 0) scaleX(-1);
	}
}
</style>
