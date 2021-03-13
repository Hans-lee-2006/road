<template>
  <div autofucos = "" class="hello" @keydown="move($event)" tabindex="0">
   <div id= "road" v-if="start == 1">
    <img id ="c1" class = "car" src = "./img/car.png" :style="{right: r + 'px'}">

    <img id ="c2" class = "car" src = "./img/car.png" :style="{right: r2 + 'px'}">

    <img id ="c3" class = "car2" src = "./img/car2.png" :style="{left: l + 'px'}">

    <img id ="c4" class = "car2" src = "./img/car2.png" :style="{left: l2 + 'px'}">
    <img id ="h" class= "human" src = "./img/human2.png" :style="{top: t + 'px',left:t2+'px'}" @click="move(10)">
    <div class="line" v-for="k  in  [1,2,3,4,5,6,7]" :key="k">
    </div>
  </div>
  <div v-if = "start == 0" id="start">
    <h1>端火鍋模擬器</h1>
    <button @click="start = 1">start</button>
  </div>
  <div v-if = "start == 2" id="start">
    <h1>恭喜你成功過關</h1>
    <a id="rickroll" href="https://youtu.be/dQw4w9WgXcQ">重新開始</a>
  </div>
  <button class="control" id="up" @click="t -= 30; maybe()" v-show="start==1">up</button>
  <button class="control" id="down" @click="t += 10; maybe()" v-show="start==1">down</button>
  <button class="control" id="left" @click="t2 -= 2; maybe()" v-show="start==1">left</button>
  <button class="control" id="right" @click="t2 += 2; maybe()" v-show="start==1">right</button>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      r: 0,
      l: 0,
      t: 400,
      r2: 400,
      l2: 400,
      t2: window.innerWidth / 2,
      v1:16,
      v2:1,
      start:false
    }
  },
  methods: {
    go() {
      this.r +=this.v1
      this.l +=this.v1+0.57
      if (this.r >= Math.max(window.innerWidth, 800)) {
        this.r = 0;
        this.v1=1+Math.random()
      }
      if (this.l >= Math.max(window.innerWidth, 800)) {
        this.l = 0;
      }
      this.r2 +=this.v2
      this.l2 +=this.v2+1
      if (this.check()){
        alert('你被撞死了')
        this.t=400
      }
      if (this.r2 >= Math.max(window.innerWidth, 800)) {
        this.r2 = 0;
         this.v2=1+Math.random()
      }
      if (this.l2 >= Math.max(window.innerWidth, 800)) {
        this.l2 = 0;
      }
    },
    collide: function (el1, el2) {
      var rect1 = el1.getBoundingClientRect();
      var rect2 = el2.getBoundingClientRect();

      return !(
        rect1.top > rect2.bottom - 150 ||
        rect1.right < rect2.left + 50 ||
        rect1.bottom < rect2.top + 150 ||
        rect1.left > rect2.right - 50
      );
    },
    check(){
      var ans = false
      var h = document.getElementById('h')
      var c1 = document.getElementById('c1')
      var c2 = document.getElementById('c2')
      var c3 = document.getElementById('c3')
      var c4 = document.getElementById('c4')
      ans = this.collide(h, c1) || this.collide(h, c2) || this.collide(h, c3) || this.collide(h, c4)
      return ans
    },
    move(e) {
      if(e.which == 38) {
        this.t -= 10
      }
      if (e.which == 40) {
        this.t += 10
      }
      if(e.which == 37) {
        this.t2 -= 1
      }
      if (e.which == 39) {
        this.t2 += 1
      }
      this.maybe()
    },
    maybe() {
      if (this.t <=20){
        this.start=2
      }
    }
  },
  mounted() {
    setInterval(this.go, 15)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.hello {
  width: 100vw;
  overflow: hidden;
}

#road {
  width: 100%;
  overflow: hidden;
  margin: 5vh auto;
  height: 400px;
  background-color: #363636;
}
.line{
 width: 10%;
 margin:190px 2%;
 display: inline-block;
 height: 10px;
 background-color:white;
}
.car{
  position: absolute;
  width: 250px;
  right:0;
}
.car2{
  position: absolute;
  width: 250px;
  left:0;
  top: 280px;
}
.human{
  position: absolute;
  width: 150px;
  left: 48vw
}

button {
  font-size: 66px;
}
#start{
  width: 100%;
  height: 100vh;
  display:flex;
  align-items: center;
  justify-content: center;
  flex-direction: column; 
}
@media screen and (min-width: 461px) {
  .thin-only {
    display: none !important;
  }
}
@media screen and (min-width: 461px) {
  .thin-only {
    display: none !important;
  }
}
.control{
  position:fixed;
}
#up{
  top: 8em;
  left:;
}
#down{
 top: 9.2em;
 left: 11em;
}
#left{
 top: 9em;
 left: 9.5em;
}
#right{
top: 9em;
 left: 13.6em;
}
#rickroll{
  border: 1px solid black;
  background-color: #ccc;
  padding: 5px;
  color: black;
  text-decoration: none;
  font-size: 25px
}
</style>
