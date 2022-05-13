<template>
  <v-app>
    <v-app-bar app color="blue" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          :src="require('./assets/logo.png')"
          transition="scale-transition"
          width="40"
        />
        <h3>Gridify</h3>
      </div>
    </v-app-bar>

    <v-main>
      <main-component />
    </v-main>
  </v-app>
</template>

<script>
/* eslint-disable */
import MainComponent from "./components/main.component.vue";

export default {
  name: "App",

  components: {
    MainComponent,
  },

  data: function () {
    return {};
  },
  methods: {},
  created() {},
};
</script>

<style lang="scss">
.grid {
  resize: both;
  height: 80vh;
  display: grid;
  grid-template-columns: repeat(16, 1fr);
  grid-template-rows: repeat(16, 1fr);

  &--item {
    max-height: 35px;
    max-width: 35px;
    position: relative;
    width: 35px;
    height: 35px;
    border: 1px solid #ddd;
    text-align: center;
  }
  .resizer {
    top: 0;
    left: 0;
    cursor: pointer;
    min-width: 35px;
    min-height: 35px;
    border: gray thin solid;
    background-color: gray;
    position: absolute;
    overflow: hidden;
    opacity: 0.8;
    z-index: 1;
    resize: both;
  }
  .hide {
    display: none;
  }
}
</style>
