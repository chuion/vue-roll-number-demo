<template>
  <span :class="blockName" :is-animation="isAnimation">
    {{ currentNumber }}
  </span>
</template>

<script>
export default {
  props: {
    numberValue: {
      type: String,
      required: true,
    },
    animDuration: {
      type: Number,
      default: 3000,
    },
    animInterval: {
      type: Number,
      default: 60,
    },
    blockName: {
      type: String,
      default: "roll-number",
    },
  },
  data() {
    return {
      isAnimation: false,
      currentNumber: this.numberValue,
      intervalID: -1,
      totalTime: 0
    };
  },
  watch: {
    numberValue(newNumber, oldNumber) {
      console.log("in num");
      console.log(newNumber);
      if (newNumber !== oldNumber) {
        console.log("in num init");
        this.$nextTick(() => {
            this.initialize();
        });
      }
    },
    animDuration(newVal) {
      console.log("in aim");
      console.log(newVal);
      if (!isFinite(newVal)) {
        console.log("in aim init");
        this.isAnimation = false;
        this.initialize();
      }
    },
  },
  created() {
    this.initialize();
  },
  methods: {
    initialize() {
      if (this.isAnimation) {
        return;
      }
      this.intervalID && clearInterval(this.intervalID)
      this.isAnimation = true;
      this.totalTime = 0;
      this.intervalID = setInterval(() => {
        this.totalTime += this.animInterval;
        let newNumber = "";
        for (let i = 0; i < this.numberValue.length; i++) {
          if (this.isUpdateTime(i, this.totalTime)) {
            newNumber += this.numberValue[i];
          } else if (this.isSeparator(i)) {
            newNumber += this.numberValue[i];
          } else {
            newNumber += this.getRandomInt(0, 9) + "";
          }
        }
        console.log(this.totalTime)
        if (this.totalTime > this.animDuration) {
          clearInterval(this.intervalID);
          this.isAnimation = false;
          this.currentNumber = this.numberValue;
        } else {
          this.currentNumber = newNumber;
        }
      }, this.animInterval);
    },
    isUpdateTime(index, totalTime) {
      const interval = this.numberValue.length;
      return (
        this.animDuration - this.animInterval * (index + 1) * interval <
        totalTime
      );
    },
    isSeparator(index) {
      return !Number.isInteger(parseInt(this.numberValue[index], 10));
    },
    getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
  },
};
</script>