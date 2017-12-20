<template>
  <div id="app">
    <textarea v-model="textareaStr"></textarea>
    <div v-html="text"></div>
    <button @click="renderMd">生成Markdown</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      textareaStr: '',
      text: ''
    }
  },
  methods: {
    renderMd () {
      axios({
        method: 'post',
        url: 'https://api.github.com/markdown',
        data: {
          'text': this.textareaStr,
          'mode': 'gfm',
          'context': 'github/gollum'
        }
      })
      .then((res) => {
        this.text = res.data
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
