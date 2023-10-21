<template>
  <div class="container">
        <NavComp></NavComp>
        <RouterView></RouterView>
  </div>
</template>
 
<script>
import NavComp from './components/NavComp.vue';

export default {
  name: 'App',
  components:{
    NavComp
}
}
</script>


<style scoped>
container{
  background-color: #293133;
}
</style>
