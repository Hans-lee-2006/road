<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
   <div id= "road">
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#road {
  width: 100% ;
  margin: 7em auto;
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
</style>
