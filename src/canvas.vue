<template>
  <div id="canvasLine">
    <div
      class="mark"
      id="mark"
      @mousedown="getCurrentPosition($event)"
      @mouseout="leave()"
      @mousemove="move($event)"
      @mouseup="leave()"
    ></div>
    <canvas id="canvasId" width="100" height="300"></canvas>
  </div>
</template>

<script>
export default {
  name: "",

  data() {
    return {
      height: 300,
      id: "canvasId",
      isEnter: false,
      currentClickEndNum: null,
      color: "green",
      arr: [
        {
          start: 100,
          end: 100,
        },
        {
          start: 200,
          end: 200,
        },
        {
          start: 300,
          end: 300,
        },
        {
          start: 400,
          end: 400,
        },
      ],
    };
  },
  computed: {},
  watch: {
    arr: {
      deep: true,
      handler() {
        this.clearCanvas();
        this.reload();
      },
    },
    color: {
      deep: true,
      handler() {
        this.clearCanvas();
        this.reload();
      },
    },
  },
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {
    this.reload();
  },
  beforeUpdate() {},
  updated() {},
  beforeDestroy() {},
  destroyed() {},
  methods: {
    leave() {
      document.getElementById("mark").style = "cursor:default";
      this.isEnter = false;
      this.currentClickEndNum = null;
      this.reload();
    },
    getCurrentPosition(e) {
      //   let a = 0;
      //   if (
      //     document.documentElement &&
      //     document.documentElement.scrollTop
      //   ) {
      //     a = document.documentElement.scrollTop;
      //   }
      let top =
        e.y +
        (document.documentElement.scrollTop || 0) -
        document.getElementById("canvasLine").offsetTop;
      console.log(top);
      let current = this.arr.find(
        (item) => item.end < top + 5 && item.end > top - 5
      );
      console.log(current);
      if (current) {
        this.currentClickEndNum = current.end;
        this.reload();
        this.isEnter = true;
      }
    },
    move(e) {
      if (this.isEnter) {
        let top = this.currentClickEndNum;
        let current = this.arr.find((item) => item.end === top);
        if (current) {
          current.end =
            e.y +
            (document.documentElement.scrollTop || 0) -
            document.getElementById("canvasLine").offsetTop;
          document.getElementById("mark").style = "cursor:s-resize";
          this.reload();
        }
      }
    },
    // getCanvasHeight(){
    //   this.height  = document.getElementById('canvasLine').offsetHeight;
    // },
    reload() {
      console.log("ss", this.currentClickEndNum);
      let arr = this.arr;
      if (arr.length !== 0) {
        var canvas = document.getElementById(this.id);

        canvas.height = document.getElementById("canvasLine").offsetHeight;
        arr.forEach((ele) => {
          let color = this.color;
          if (this.currentClickEndNum && this.currentClickEndNum === ele.end) {
            console.log("red");
            color = "red";
          }
          this.arrow_line(this.id, 0, 0, 0, ele.start, 100, ele.end, color);
        });
      } else {
        this.clearCanvas();
      }
    },
    arrow_line(canId, ox, oy, x1, y1, x2, y2, color) {
      //参数说明 canvas的 id ，原点坐标  第一个端点的坐标，第二个端点的坐标
      var sta = new Array(x1, y1);
      var end = new Array(x2, y2);
      var canvas = document.getElementById(canId);
      // canvas.height = 2000 || document.getElementById('canvasLine').offsetHeight;
      // console.log(canvas)
      // debugger ;
      if (canvas == null) return false;
      var ctx = canvas.getContext("2d");
      ctx.strokeStyle = color || "#000";
      //画线
      ctx.beginPath();

      ctx.translate(ox, oy, 0); //坐标源点
      // ctx.setLineDash([5, 15]);

      ctx.moveTo(sta[0], sta[1]);
      ctx.lineTo(end[0], end[1]);
      ctx.fill();
      ctx.fillStyle = color || "#000";
      ctx.stroke();
      ctx.save();
      //画箭头
      ctx.translate(end[0], end[1]);
      //我的箭头本垂直向下，算出直线偏离Y的角，然后旋转 ,rotate是顺时针旋转的，所以加个负号
      var ang = (end[0] - sta[0]) / (end[1] - sta[1]);
      ang = Math.atan(ang);
      if (end[1] - sta[1] >= 0) {
        ctx.rotate(-ang);
      } else {
        ctx.rotate(Math.PI - ang); //加个180度，反过来
      }
      ctx.lineTo(-5, -10);
      ctx.lineTo(0, -5);
      ctx.lineTo(5, -10);
      ctx.lineTo(0, 0);
      ctx.fill(); //箭头是个封闭图形
      ctx.restore(); //恢复到堆的上一个状态，其实这里没什么用。
      ctx.closePath();
    },
    clearCanvas() {
      var c = document.getElementById(this.id);
      var cxt = c.getContext("2d");
      cxt.clearRect(0, 0, c.width, c.height);
    },
  },
};
</script>

<style lang="less" scoped>
#canvasLine {
  width: 100px;
  height: 500px;
  border: 5px solid pink;
  position: relative;
  .mark {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.212);
  }
}
</style>
