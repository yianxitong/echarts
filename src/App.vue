<template>
  <div id="app">
    <div class="linkBar">
      <router-link class="map" to="/map">Domestic NCP map</router-link>
      <a-divider type="vertical" />
      <router-link class="mapWorld" to="/mapWorld">Global NCP map</router-link>
      <a-divider type="vertical" />
      <router-link class="line" to="/line">Domestic NCP trend</router-link>
      <a-divider type="vertical" />
      <router-link class="line" to="/lineWorld">Global NCP trends</router-link>
    </div>
    <div class="linkBar">
      
    </div>
    <div class="chart">
      <router-view></router-view>
    </div>
  </div>
</template>

<style>
  /* #app{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  } */
  #app {
    text-align: center;
  }
  /* .map{
   color: #ccc;
   font-size: 20px;
   margin: 0 auto;
   text-align: center;
  } */
  .linkBar{
    margin: 50px 0;
    font-size: 26px;
  }
  .router-link-active{
    color: rgb(96, 174, 138);
  }
</style>
