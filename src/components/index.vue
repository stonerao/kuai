<template>
    <div class="app-box" id="app-box">
        <div class="center" v-html="htmlBox" v-if="!isGood">

        </div>
        <div class="center" v-else>
            <span class="click-p" @click="jx">点击有惊喜</span>
            <canvas id="c"></canvas>
        </div>
    </div>
</template>

<script>
import $ from "jquery";
export default {
  data() {
    return {
      arr: [
        ["庞婷婷"],
        [ 
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
          "她是谁",
        ],
        ["我媳妇儿", "媳妇儿"],  
        ["我是媳妇儿是一个"], 
        ["美丽","美丽","美丽","美丽","美丽","美丽","美丽","美丽","美丽","美丽"], 
        ["善良","善良","善良","善良","善良"],  
        ["优雅","优雅","优雅","优雅","优雅","优雅","优雅","优雅","优雅","优雅","优雅","优雅"], 
        ["脱俗","脱俗","脱俗","抽屉","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗","脱俗"], 
        ["可爱","可爱","可爱","可爱","可爱","可爱","可爱","可爱"], 
        ["天真","天真","抽屉","天真","天真","天真"], 
        ["温柔","温柔","温柔","温柔","温柔","温柔","温柔","温柔","温柔"], 
        ["多才","多才","多才","多才","多才","多才","多才"],  
        ["贤惠","贤惠","贤惠","贤惠","贤惠","贤惠","贤惠","贤惠","贤惠","贤惠","贤惠"],
        ["好媳妇儿"],
        ["这么好的媳妇儿"],
        ["我要娶她"],
        ["要给她买小裙裙"], 
        ["买好吃的"], 
        ["车上有礼物"], 
        ["亲爱的","媳妇"],
        ["你这么的可爱"], 
        ["漂亮"],
        ["我要送一你"]   
      ],
      htmlBox: "",
      isGood: false
    };
  },
  mounted() {
    const random = num => {
      return parseInt(Math.random() * num);
    };
    const setArea = () => {
      return {
        position: "absolute",
        top: 10 + random(50) + "%",
        "font-size": 20 + random(20) + "px",
        transform: `rotate(${random(10) - random(30)}deg) translate(${
          random(50) % 2 == 1 ? random(100) : -random(200)
        }px,0)`
      };
    };
    const demo = arr => {
      if (arr.length < 1) {
        this.isGood = true;
        setTimeout(x => {
          this.huahua();
        }, 300);
        return;
      }
      var str = "";
      arr[0].forEach(x => {
        let style = setArea();
        let s = "";
        for (var k in style) {
          if (arr[0].length == 1 && k == "transform") {
            s += `transform:translateX(-50%);`;
            continue;
          }
          s += `${k}:${style[k]};`;
        }
        str += `<span style="${s}">${x}</span>`;
      });
      this.htmlBox = str;
      console.log(str);
      setTimeout(x => {
        arr.splice(0, 1);
        demo(arr);
      }, 700);
    };
    demo(this.arr);
  },
  methods: {
    jx(){
      alert("恭喜你，拥有了老公！") 
      alert("惊喜在他那！")
    },
    huahua() {
      var canvas = document.getElementById("c");
      var context = canvas.getContext("2d");

      var a = context;
      var b = document.body;
      var c = canvas;

      document.body.clientWidth;
      var zBuffer = [];
      var SIZE = 300;
      canvas.width = window.screen.width;
      canvas.height = window.screen.height;
      var h = -350;

      function surface(a, b, c) {
        if (c > 60) {
          return {
            x:
              Math.sin(a * 7) * (13 + 5 / (0.2 + Math.pow(b * 4, 4))) -
              Math.sin(b) * 50,
            y: b * SIZE + 50,
            z:
              625 +
              Math.cos(a * 7) * (13 + 5 / (0.2 + Math.pow(b * 4, 4))) +
              b * 400,
            r: a * 1 - b / 2,
            g: a
          };
        }

        var A = a * 2 - 1;
        var B = b * 2 - 1;

        if (A * A + B * B < 1) {
          if (c > 37) {
            var j = c & 1;
            var n = j ? 6 : 4;
            var o = 0.5 / (a + 0.01) + Math.cos(b * 125) * 3 - a * 300;
            var w = b * h;
            return {
              x: o * Math.cos(n) + w * Math.sin(n) + j * 610 - 390,
              y: o * Math.sin(n) - w * Math.cos(n) + 550 - j * 350,
              z: 1180 + Math.cos(B + A) * 99 - j * 300,
              r:
                0.4 -
                a * 0.1 +
                Math.pow(1 - B * B, -h * 6) * 0.15 -
                a * b * 0.4 +
                Math.cos(a + b) / 5 +
                Math.pow(Math.cos((o * (a + 1) + (B > 0 ? w : -w)) / 25), 30) *
                  0.1 *
                  (1 - B * B),
              g: o / 1e3 + 0.7 - o * w * 3e-6
            };
          }

          if (c > 32) {
            c = c * 1.16 - 0.15;
            var o = a * 45 - 20;
            var w = b * b * h;
            var z = o * Math.sin(c) + w * Math.cos(c) + 620;
            return {
              x: o * Math.cos(c) - w * Math.sin(c),
              y: 28 + Math.cos(B * 0.5) * 99 - b * b * b * 60 - z / 2 - h,
              z: z,
              r: (b * b * 0.3 + Math.pow(1 - A * A, 7) * 0.15 + 0.3) * b,
              g: b * 0.7
            };
          }

          var o = A * (2 - b) * (80 - c * 2);
          var w =
            99 -
            Math.cos(A) * 120 -
            Math.cos(b) * (-h - c * 4.9) +
            Math.cos(Math.pow(1 - b, 7)) * 50 +
            c * 2;
          var z = o * Math.sin(c) + w * Math.cos(c) + 700;
          return {
            x: o * Math.cos(c) - w * Math.sin(c),
            y: B * 99 - Math.cos(Math.pow(b, 7)) * 50 - c / 3 - z / 1.35 + 450,
            z: z,
            r: (1 - b / 1.2) * 0.9 + a * 0.1,
            g: Math.pow(1 - b, 20) / 4 + 0.05
          };
        }
      }

      setInterval(function() {
        for (var i = 0; i < 10000; i++) {
          var part = i % 46;
          var c = part / 0.74;
          var point = surface(Math.random(), Math.random(), c);
          if (point) {
            var z = point.z;
            var x = parseInt(point.x * SIZE / z - h) - 150;
            var y = parseInt(point.y * SIZE / z - h)-50;
            var zBufferIndex = y * SIZE + x;
            if (
              typeof zBuffer[zBufferIndex] === "undefined" ||
              zBuffer[zBufferIndex] > z
            ) {
              zBuffer[zBufferIndex] = z;
              var r = -parseInt(point.r * h);
              var g = -parseInt(point.g * h);
              var b = -parseInt(point.r * point.r * -80);
              context.fillStyle = "rgb(" + r + "," + g + "," + b + ")";
              context.fillRect(x, y, 1, 1);
            }
          }
        }
      }, 0);
    }
  }
};
</script>

<style lang="less" scoped>
* {
  color: #fff;
}
.center {
  text-align: center;
  color: #fff;
}
.app-box {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: #000;
}
.click-p{
  position:absolute;
  left:5px;
  top:2px;
  font-size:12px;
  color:#ccc;

}
</style>

