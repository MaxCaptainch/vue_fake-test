<template>
  <div id="app">
    <div class="nav-bar"><h1>ЗНУ ТЕСТ</h1></div>
    <router-view/>
  
  </div>
</template>

<style>
body{
  overflow: hidden;
  margin: 0;  
  background-image:url('assets/bg4.png');
  background: cover;
}

#app{
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}

.nav-bar{
  width: 100%;
  height: 20%;
  position: relative;
  background-color: #000;
  color:white;
  text-align: center;
  margin: 0;
}

h1{
  margin: 0;  
  padding: 0;
}


</style>

