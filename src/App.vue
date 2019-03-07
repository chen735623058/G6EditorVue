<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
  *{
    font-size: 12px !important;
  }
  *, *::before, *::after {
    box-sizing: border-box;
  }
  html,body{
    margin: 0 !important;
    width: 100% !important;
    height: 100% !important;
  }

  #app{
    height: 100%;
  }
</style>
