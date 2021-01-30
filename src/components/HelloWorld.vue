<template>
  <div autofucos = "" class="hello" @keydown="move($event)" tabindex="0">
    <h1>{{ msg }}</h1>
   <div id= "road">
    <img class = "car" src = "/img/car.png" :style="{right: r + 'px'}">

    <img class = "car" src = "/img/car.png" :style="{right: r + dr + 'px'}">

    <img class = "car2" src = "/img/car2.png" :style="{left: l + 'px'}">

    <img class = "car2" src = "/img/car2.png" :style="{left: l + dl + 'px'}">
    <img class= "human" src = "/img/human.png" :style="{top: t + 'px'}" @click="move(10)">
    <div class="line" v-for="k  in  [1,2,3,4,5,6,7]" :key="k">
    </div>
  </div>
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
      dr: 400,
      dl: 400
    }
  },
  methods: {
    go() {
      this.r ++
      this.l ++
      if (this.r >= window.innerWidth) {
        this.r = -this.dr;
      }
      if (this.l >= window.innerWidth) {
        this.l = -this.dl;
      }
      this.dr += Math.floor(Math.random()*3-1)
      this.dl += Math.floor(Math.random()*3-1)
    },
    move(e) {
      if(e.which == 38) {
        this.t -= 10
      }
      if (e.which == 40) {
        this.t += 10
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
</style>
