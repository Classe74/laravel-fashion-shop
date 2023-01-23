<template>
  <h1>{{ title }}</h1>
</template>

<script>
import axios from 'axios';
  export default {
    name: 'App',
    data() {
        return {
            title: 'Hello Vue',
        }
    },
    
  }
</script>

<style lang="scss" scoped>

</style>