<template>
  <div id="app">
      <Theme :data="data" @on-changeTheme="changeTheme"></Theme>
  </div>
</template>

<script>
import Theme from './components/Theme.vue'

export default {
  name: 'app',
  components: {
      Theme
  },
  data(){
      return{
          data:[
              {name:"white",color:"#f4f4f4"},
              {name:"black",color:"#222222"},
             {name:"red",color:"#dc3b18"},
              ],
      }
  },
   methods:{
       changeTheme(item){
           document.body.style.backgroundColor = item.color;
       }
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
</style>
