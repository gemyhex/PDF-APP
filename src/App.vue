<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

/* width */
::-webkit-scrollbar {
  width: 2px;
  height: 1px;
}

/* Track */
::-webkit-scrollbar-track {
  background: transparent;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: red;
}

.accordion-button::after {
  background-image: none;
}
.accordion-button::not(.collapsed):after {
  background-image: none;
}

.row {
  margin-left: 0 !important;
  margin-right: 0 !important;
}
</style>
