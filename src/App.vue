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

.accordion-button::after {
  background-image: none;
}
.accordion-button::not(.collapsed):after {
  background-image: none;
}
.tableC {
  // border: 2px solid black;
  text-align: start;
  padding: 2px;
}
ul {
  list-style-type: none;
  border: 1px solid black;
  padding: 0 !important;
}
li {
  // padding: 10px;
  border-bottom: 1px solid black;
  max-height: 50px;
  height: 50px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.headSpan {
  position: relative;
  width: 100%;
  display: flex;
  // justify-content: center;
  // align-items: center;
  border-bottom: 1px solid black;
}
.headTitle {
  // padding: 8px;
  border-right: 1px solid black;
}
.headCon {
  // padding: 8px;
}
.row {
  margin-left: 0 !important;
  margin-right: 0 !important;
}
</style>
