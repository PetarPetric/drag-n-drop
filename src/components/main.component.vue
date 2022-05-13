<template>
  <v-container class="d-flex justify-center">
    <div ref="wrapper">
      <div @mousemove="handleResizing" class="grid">
        <div
          @dragenter="dragEnter"
          @dragleave="dragLeave"
          @dragover="dragOver"
          @drop="drop"
          class="grid--item"
          v-for="square in 256"
          :key="square"
        >
          <div
            @dragstart="dragStart"
            draggable="true"
            :class="{ hide: hide }"
            id="resizer"
            v-if="square == 1"
            class="resizer"
          ></div>
        </div>
      </div>
    </div>
  </v-container>
</template>

<script>
/*eslint-disable*/
let resizer;
let grid;

export default {
  name: "MainComponent",
  data: () => ({
    width: 0,
    height: 0,
    maxWidth: null,
    maxHeight: null,
    gridPosition: null,
    hide: false,
  }),
  watch: {},
  methods: {
    dragStart(e) {
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData("text/plain", e.target.id);
      setTimeout(() => {
        this.hide = true;
      }, 0);
    },
    dragEnter(e) {
      e.preventDefault();
    },

    dragOver(e) {
      e.preventDefault();
    },

    dragLeave(e) {},

    drop(e) {
      const id = e.dataTransfer.getData("text/plain");
      const draggable = document.getElementById(id);

      // add it to the drop target
      e.target.appendChild(draggable);
      this.hide = false;
    },
    // its not advised to do this stuff
    getPositions() {
      let resizerPosition = {
        bottom: resizer.getBoundingClientRect().bottom,
        right: resizer.getBoundingClientRect().right,
      };
      this.gridPosition = {
        bottom: grid.getBoundingClientRect().bottom,
        right: grid.getBoundingClientRect().right,
      };
      if (resizerPosition.right > this.gridPosition.right) {
        resizer.style.width = `${
          this.width - Math.abs(this.gridPosition.right - resizerPosition.right)
        }px`;
      }
      if (resizerPosition.bottom > this.gridPosition.bottom) {
        resizer.style.height = `${
          this.height -
          Math.abs(this.gridPosition.bottom - resizerPosition.bottom)
        }px`;
      }
    },
    handleResizing(e) {
      if (e.target.className === "resizer") {
        this.maxWidth = this.$refs.wrapper.clientWidth;
        this.maxHeight = this.$refs.wrapper.clientHeight;
        grid = document.querySelector(".grid");
        resizer = document.querySelector(".resizer");
        // since width and height of squares are 35 px 
        this.height = Math.round(resizer.offsetHeight / 35) * 35;
        this.width = Math.round(resizer.offsetWidth / 35) * 35;
        resizer.style.height = `${this.height}px`;
        resizer.style.width = `${this.width}px`;
        this.getPositions();
      }
    },
  },
  mounted() {},
};
</script>
