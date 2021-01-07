<template>
  <div>
    <vue-p5
      @preload="preload"
      @setup="setup"
      @draw="draw"
      @keypressed="keyPressed"
      @mousemoved="mouseMoved"
      @mousedragged="mouseDragged"
    >
    </vue-p5>
  </div>
</template>

<script>
import VueP5 from "vue-p5";

export default {
  name: "p5-example",
  components: {
    "vue-p5": VueP5,
  },
  data: () => ({}),
  methods: {
    setup(sketch) {
      sketch.createCanvas(
        window.screen.width,
        window.screen.height,
        sketch.WEBGL
      );
    },
    draw(sketch) {
      sketch.background(250);
      sketch.rotateY(sketch.frameCount * 0.01);

      for (let j = 0; j < 5; j++) {
        sketch.push();
        for (let i = 0; i < 80; i++) {
          sketch.translate(
            sketch.sin(sketch.frameCount * 0.001 + j) * 100,
            sketch.sin(sketch.frameCount * 0.001 + j) * 100,
            i * 0.1
          );
          sketch.rotateZ(sketch.frameCount * 0.002);
          sketch.push();
          sketch.sphere(8, 6, 4);
          sketch.pop();
        }
        sketch.pop();
      }
    },
  },
};
</script>
