<template>
  <div id="app">
    <left-nav></left-nav>
    <div class="main">
	    <router-view/>
    </div>
  </div>
</template>

<script>
	import leftNav from "@/components/leftNav"
export default {
  name: 'App',
  components:{
  	leftNav
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
*{
	margin: 0;
	padding: 0;
}
</style>
