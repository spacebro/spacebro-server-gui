<template>
  <div id="app">
    <label for="port">port:</label>
    <input type="number" v-model="port" id="port">
    <pre>ip: <span>{{ ip }}</span></pre>
    <button type="button" :disabled="started" @click="initSpacebro">start server</button>
    <div class="info" v-show="started">server started</div>
  </div>
</template>

<script>
  const ip = require('ip')

  export default {
    name: 'spacebro-server-gui',
    data () {
      return {
        ip: '127.0.0.1',
        port: 8888,
        started: false
      }
    },
    mounted () {
      this.ip = ip.address()
    },
    methods: {
      initSpacebro () {
        require('electron').ipcRenderer.send('init-server', this.port)
        this.started = true
      }
    }
  }
</script>

<style>
  @import './style/css/reset';
  @import './style/css/kiosk';
  /* CSS */
  * {
    margin: 0;
    padding: 0;
  }
  body {
    background: #1A1A1A;
    font-family: monospace;
    color: #F0F0F0;
  }
  #app {
    width: 80%;
    max-width: 980px;
    margin: 1em auto;
    text-align: center;
  }
  input, pre, #app > div {
    margin: 1em auto;
  }
  pre {
    background: #0F0F0F;
    padding: 1em;
    width: 80%;
  }
  pre > span {
    user-select: auto;
  }
  button {
    padding: 0.15em 1em 0.3em;
  }
  input {
    border: none;
    border-radius: 0.2em;
    padding: 0.25em 0 0.25em 1em;
    width: 5em;
  }
</style>
