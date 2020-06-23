<template>
  <div>
    <span v-if="minutes < 10">0</span>{{ minutes }}:<span v-if="seconds < 10">0</span>{{ seconds }}
  </div>
</template>
<script>
export default {

  data() {
    return {
      minutes: 0,
      seconds: 0,
      elapsed: 0,
    };
  },
  created() {
    const urlParams = new URLSearchParams(window.location.search);
    const urlMinutes = urlParams.get('minutes');
    this.minutes = Number(urlMinutes) || 10;
    setInterval(this.countDown, 1000);
  },
  methods: {
    countDown: function() {
      if(this.minutes == 0 && this.seconds == 0) return;
      if(this.seconds == 0) {
        this.seconds = 59;
        this.minutes--;
      } else {
        this.seconds--;
      }

    }
  },
};
</script>

<style lang="scss" scoped>
div {
  // background-color: #b350124d;
  // margin-top: 100px;
  margin-left: auto;
  margin-right: auto;
  font-size: 6rem;
  letter-spacing: 0.2em;
}
</style>