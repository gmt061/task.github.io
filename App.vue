<template>
  <div id="app">
    <div class="Fon">
      <div class="backColor">
       <VRowDevelop />
     </div>
    </div>

    <router-view/>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import VRowDevelop from '../src/components/v-row-develop.vue'
export default {
  components: {
    VRowDevelop
  },
  methods: {

  }
}
</script>

<style >
.btnbtn{
  background-color: red;
}
.Fon{
  display: flex;
  justify-content: center;
}
.backColor{
position: relative;
width: 960px;
height: 1384px;
background: #1E1E1E;
}
</style>
