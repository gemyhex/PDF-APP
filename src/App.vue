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
.tableC {
  text-align: start;
  padding: 2px;
  display: flex;
  overflow: scroll;
  ul {
    min-width: 50%;
    li {
      border-bottom: 1px solid black;
      height: 100px;
      text-align: center;
      overflow: hidden;
    }
  }
}
ul {
  list-style-type: none;
  border: 1px solid black;
  padding: 0 !important;
}
li {
  border-bottom: 1px solid black;
}
.headSpan {
  border-bottom: 1px solid black;
}
.headTitle {
  text-overflow: ellipsis;
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
