<template>
  <div id="app">
    <router-view class="wallet" />
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 110vh;
  display: flex;
  justify-content: center;
  background: rgb(219, 219, 219);
}
.wallet {
  width: 26rem;
  height: 56rem;
  min-height: min-content;
  background: white;
  margin: 1rem;
  -webkit-box-shadow: 6px 6px 26px -8px rgba(0, 0, 0, 0.52);
  -moz-box-shadow: 6px 6px 26px -8px rgba(0, 0, 0, 0.52);
  box-shadow: 6px 6px 26px -8px rgba(0, 0, 0, 0.52);
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
