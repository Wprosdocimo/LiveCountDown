<template>
  <div id="app">
    <div class="content">
      <h1>{{ title }}</h1>
      <h2 v-html="stream_title"></h2>
      <h3 v-html="stream_subtitle"></h3>
      <Clock />
      <p v-html="stream_paragraph"></p>
    </div>
  </div>
</template>

<script>
import Clock from "./components/clock.vue";

export default {
  name: "App",
  
  components: {
    Clock
  },
  async mounted() {
    const data = await fetch("data.json");
    const config = await data.json();
    this.stream_title = config["stream-title"];
    this.stream_subtitle = config["stream-subtitle"];
    this.stream_paragraph = config["stream-paragraph"];
  },
  data() {
    return {
      stream_title: "",
      stream_subtitle: "",
      stream_paragraph: ""
    };
  },
  computed: {
    title() {
      const urlParams = new URLSearchParams(location.search);
      return urlParams.get("title") || "O live coding está começando!";
    }
  }
};
</script>

<style lang="scss">
@import "./assets/css/normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Fira+Code&family=Satisfy&display=swap");
#app {
  font-family: "Satisfy", cursive;
  width: 100vw;
  height: 100vh;
  background-image: url("./assets/img/lighthouse.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  .content {
    color: #fff;
    font-size: 2rem;
    max-width: 1000px;
    height: 60vh;
    padding-bottom: 70px;
    margin-left: 100px;
    text-align: center;
    > * {
      text-shadow: -2px 4px 10px #2c19ff;
    }
    h1 {
      max-width: 765px;
      font-size: 4rem;
      text-align: center;
      margin: auto;
      margin-bottom: 70px;
    }
    h2 {
      font-size: 3rem;
      text-align: center;
      margin: auto;
      max-width: 1000px;
      font-weight: lighter;
    }
    h3 {
      font-size: 1.8rem;
      text-align: center;
      margin: 10px auto 70px;
      max-width: 750px;
      color: #64ff4d;
      font-family: "Fira Code", monospace;
    }
    p {
      position: absolute;
      /* line-height: 1.5rem; */
      font-size: 1.8rem;
      bottom: 0px;
      max-width: 1120px;
      font-family: "Fira Code", monospace;
      /* text-shadow: 0px 2px 0px #B34F12; */
    }
  }
}
</style>
