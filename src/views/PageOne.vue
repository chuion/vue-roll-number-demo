<template>
  <div style="width: 320px; margin: 0 auto">
    <DigitRoll ref="digitroll" :rollDigits="digits" :flipStra="true" />
    <input type="text" v-model="input" />
    <button @click="changeDigit">click me</button>
  </div>
</template>

<script>
import DigitRoll from "@/components/DigitRoll";

export default {
  name: "PageOne",
  components: {
    DigitRoll,
  },
  data() {
    return {
      digits: "000",
      input: ""
    };
  },

  methods: {
    formatInput(str) {
      const TARGET_LEN = 3;
      const strLen = str.length;
      let res = "";
      for (let i = 0; i < TARGET_LEN - strLen; i++) {
        res += "0";
      }
      console.log(res + str);
      return (res + str).split("").map((it, idx) => ({
        value: it,
        dur: 600 + idx * 300,
      }));
    },
    changeDigit() {
      clearInterval(this.timer)
      this.$refs.digitroll.setDigit(this.formatInput(this.input));
      // this.$refs.digitroll.setDigit([
      //   {
      //     value: 2,
      //     dur: 600,
      //   },
      //   {
      //     value: 4,
      //     dur: 900,
      //   },
      //   {
      //     value: 6,
      //     dur: 1200,
      //   },
      //   {
      //     value: 8,
      //     dur: 1500,
      //   },
      // ]);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
