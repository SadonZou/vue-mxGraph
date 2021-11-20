<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
  export default {
    name: 'App'
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }

  #app {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
  }

  ::-webkit-scrollbar {
    width: 5px; /* 纵向滚动条*/
    height: 7px; /* 横向滚动条 */
    background-color: #fff;
    transition: opacity 120ms ease-out;
    border-radius: 10px;
  }

  /*定义滚动条轨道 内阴影*/
  ::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0);
    background-color: #fff;
    border-radius: 10px;
  }

  /*定义滑块 内阴影*/
  ::-webkit-scrollbar-thumb {
    -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0);
    background-color: #D5D5D5;
    border-radius: 10px;
  }
</style>
