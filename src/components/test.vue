<template>
  <section>
    <canvas id="canvas" width="1229" style="width:100%;height:100%;" height="900"></canvas>
  </section>
</template>
<script>
export default {
  name: "uxCanvasBg",

  data() {
    return {
      canvas: null,

      ctx: null,

      w: 0,

      h: 0,

      circles: []
    };
  },

  computed: {},

  watch: {},

  destroyed() {},

  methods: {
    newobject(x, y) {
      var object = new Object();

      object.x = x;

      object.y = y;

      object.r = Math.random() * 3;

      object._mx = Math.random();

      object._my = Math.random();

      this.circles.push(object);
    },

    drawCircle(obj) {
      this.ctx.beginPath();

      this.ctx.arc(obj.x, obj.y, obj.r, 0, 360);

      this.ctx.closePath();

      this.ctx.fillStyle = "rgba(204, 204, 204, 0.3)";

      this.ctx.fill();
    },

    drawLine(obj1, obj) {
      let dx = obj1.x - obj.x;

      let dy = obj1.y - obj.y;

      let d = Math.sqrt(dx * dx + dy * dy);

      if (d < 60) {
        this.ctx.beginPath();

        this.ctx.lineWidth = 0.5;

        this.ctx.moveTo(obj1.x, obj1.y); //start

        this.ctx.lineTo(obj.x, obj.y); //end

        this.ctx.closePath();

        this.ctx.strokeStyle = "rgba(204, 204, 204, 0)";

        this.ctx.stroke();
      }
    },

    move(obj) {
      obj._mx = obj.x < this.w && obj.x > 0 ? obj._mx : -obj._mx;

      obj._my = obj.y < this.h && obj.y > 0 ? obj._my : -obj._my;

      obj.x += obj._mx / 2;

      obj.y += obj._my / 2;
    },

    draw() {
      this.ctx.clearRect(0, 0, this.w, this.h);

      for (let i = 0; i < this.circles.length; i++) {
        this.move.call(this.circles[i], this.circles[i]);

        this.drawCircle.call(this.circles[i], this.circles[i]);

        for (let j = i + 1; j < this.circles.length; j++) {
          this.drawLine.call(this.circles[i], this.circles[i], this.circles[j]);
        }
      }

      requestAnimationFrame(this.draw);
    },

    init(num) {
      for (var i = 0; i < num; i++) {
        this.newobject(Math.random() * this.w, Math.random() * this.h);
      }

      this.draw();
    }
  },

  created: function() {},

  components: {
    // uxLogForm
  },

  mounted() {
    window.requestAnimationFrame =
      window.requestAnimationFrame ||
      window.mozRequestAnimationFrame ||
      window.webkitRequestAnimationFrame ||
      window.msRequestAnimationFrame;

    this.canvas = document.getElementById("canvas");

    this.ctx = canvas.getContext("2d");

    this.w = canvas.width = canvas.offsetWidth;

    this.h = canvas.height = canvas.offsetHeight;

    this.init(350);
  }
};
</script>
<style lang="scss" scoped>
section {
  margin: 0;

  height: 100%; // min-height: 680px;

  width: 100%;

  overflow: hidden;
}

canvas {
  display: inline-block;

  width: 100%;

  height: 100%;

  padding: 0;

  margin: 0;
}
</style>