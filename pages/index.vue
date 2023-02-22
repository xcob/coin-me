<template>
  <b-container align-h="center" align-v="center" id="chartContainer">
    <b-row>
      <b-col align-self="center">
        <Charts />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  export default {
    name: 'IndexPage'
  }

</script>

<style>
  #chartContainer{
    width: 100vw;
    height: 100vh;
  }

</style>
