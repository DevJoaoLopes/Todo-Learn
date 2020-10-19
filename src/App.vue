<template>
  <div id="app">
    <h1>Lista de Tarefas</h1>
  </div>
</template>

<script>
export default {
  name: 'app',
};
</script>

<style>
body {
  background: #34e89e; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #0f3443,
    #34e89e
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #0f3443,
    #34e89e
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  font-family: "Lato", sans-serif;
  color: #ffffff;
}

#app {
  display: flex;
  flex: 1;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-size: 3rem;
  font-weight: 300;
}
</style>
