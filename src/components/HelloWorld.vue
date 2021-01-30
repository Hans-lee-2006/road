<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
   <div id= "road">
    <img class = "car" src = "/img/car.png" :style="{right: r + 'px'}">
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
      r: 0
    }
  },
  methods: {
    go() {
      this.r ++
    }
  },
  mounted() {
    setInterval(this.go, 25)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#road {
  width: 100% ;
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
</style>
