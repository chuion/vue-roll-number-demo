<template>
  <div class="custom-roll-number__wrap">
    <ul
      class="custom-roll-number"
      :style="{
        animation: status
          ? `${animateName}up 1s linear ${
              status === 'start' ? 'infinite' : 'forwards'
            }`
          : 'none',
      }"
    >
      <li class="counter-item">0</li>
      <li class="counter-item">1</li>
      <li class="counter-item">2</li>
      <li class="counter-item">3</li>
      <li class="counter-item">4</li>
      <li class="counter-item">5</li>
      <li class="counter-item">6</li>
      <li class="counter-item">7</li>
      <li class="counter-item">8</li>
      <li class="counter-item">9</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RollCounter",
  props: {
    num: {
      type: String,
      default: -1,
    },
    infiniteRoll: {
      type: Boolean,
      default: false,
    },
    animateName: {
      type: String,
      default: "row",
    },
  },
  data() {
    return {
      status: "",
      height: null,
    };
  },
  watch: {
    infiniteRoll(val) {
      if (val) {
        this.init();
      }
    },
    num() {
      this.getNumber();
    },
  },
  mounted() {
    this.height = document.querySelector(".custom-roll-number").offsetHeight;
    this.init();
  },

  methods: {
    addKeyFrames(y) {
      var style = document.createElement("style");
      var keyFrames = `
          @keyframes ${this.animateName}up {
              0% {
                  -webkit-transform: translate3d(0, 0, 0);
                  transform: translate3d(0, 0, 0);
              }
              100% {
                  -webkit-transform: translate3d(0, ${y}, 0);
                  transform: translate3d(0, ${y}, 0);
              }
          }
    `;
      style.innerHTML = keyFrames;
      document.getElementsByTagName("head")[0].appendChild(style);
    },
    init() {
      this.addKeyFrames("-" + this.height + "px"); // 设置keyframes
      this.status = "start";
    },
    getkeyframes(name) {
      var animation = {};
      // 获取所有的style
      var ss = document.styleSheets;
      for (var i = 0; i < ss.length; ++i) {
        const item = ss[i];
        if (
          item.cssRules[0] &&
          item.cssRules[0].name &&
          item.cssRules[0].name === name
        ) {
          animation.cssRule = item.cssRules[0];
          animation.styleSheet = ss[i];
          animation.index = 0;
        }
      }
      return animation;
    },
    getNumber() {
      const rowupKeyframes = this.getkeyframes(`${this.animateName}up`);
      rowupKeyframes.styleSheet.deleteRule(rowupKeyframes.index);
      const y = "-" + (this.height / 10) * this.num + "px";
      const newFrame = `
          @keyframes ${this.animateName}up {
              0% {
                  -webkit-transform: translate3d(0, 0, 0);
                  transform: translate3d(0, 0, 0);
              }
              100% {
                  -webkit-transform: translate3d(0, ${y}, 0);
                  transform: translate3d(0, ${y}, 0);
              }
          }
    `;
      rowupKeyframes.styleSheet.insertRule(newFrame, rowupKeyframes.index);
      this.status = "stop";
    },
  },
};
</script>

<style lang="scss" scoped>
.custom-roll-number__wrap {
  width: 30px;
  height: 20px;
  overflow: hidden;
  border: 1px solid black;
  .custom-roll-number {
    width: 30px;
    list-style: none;
    padding: 0;
    margin: 0;
    li.counter-item {
      width: 30px;
      height: 20px;
      line-height: 20px;
      font-size: 16px;
    }
  }
}
</style>