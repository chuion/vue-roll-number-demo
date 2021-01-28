<template>
  <div>
    <roll-number :number-value="num" :animDuration="animDuration" />
    <input type="text" v-model="input" />
    <button @click="start">start roll</button>
    <button @click="changeDigit">get it</button>
  </div>
</template>

<script>
import RollNumber from "../components/RollNumber";
export default {
  name: "PageTwo",
  components: {
    RollNumber,
  },
  data() {
    return {
      animDuration: 0,
      input: "000",
      num: '000'
    };
  },
  methods: {
    changeDigit() {
      this.animDuration = 3000;
      this.num = this.input 
    },
    start() {
        this.input = ''
        this.num = '000';
        this.animDuration = Infinity
    }
  },
};
</script>