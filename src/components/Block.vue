<template>
<p>Hello</p>
<div class="line" ref="line"></div>
  <div @click="stopTimer" class="block" v-if="showBlock">click me</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  mounted() {
    //   lifecycle hook for when a component is initially mounted
    // Can be used for creating api calls
    console.log("component is mounted");
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
      console.log(this.delay);
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
        this.$refs.line.style.width = `${this.reactionTime}px`
      }, 10);
    },
    stopTimer() {
        clearInterval(this.timer);
        // you can use emit to send stuff back to a parent element, with the name of the action as the first argument and the remaining argument as the data you want to pass back from the child elements  
        this.$emit('end', this.reactionTime)
        console.log(this.reactionTime);
    },
  },
  updated() {
    //   This is fired when any of the properties available on the component changes
    console.log("component is updated");
  },

  unmounted() {
    console.log("component is unmounted");
  },
};
</script>

<style>
.block {
  width: 400px;
  margin: 40px auto;
  padding: 100px 0;
  color: white;
  text-align: center;
  border-radius: 20px;
  background-color: #0faf87;
}

.line{
  height: 10px;
  width: 0px;
  background-color: #0faf87;
  max-width: 1000px;
}
p{
    color: black;
}
</style>