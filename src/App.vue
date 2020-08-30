<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/Helloworld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app{
  background-image: url("./assets/cold-bg.png");
  background-size: cover;
  min-height: 97.5vh;

}
</style>