<template>
  <div id="app">
    <h1>Markdon Online</h1>
    <textarea class="textarea" v-model="textareaStr"></textarea>
    <button class="button" @click="renderMd">生成Markdown</button>
    <div v-html="text"></div>
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
*{
  user-select: none;
}
html{
  -webkit-tap-highlight-color: transparent;
  -webkit-text-size-adjust: 100%;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.textarea{
  width: 100%;
  box-sizing: border-box;
  border-radius: 5px;
  height: 100px;
}

.button{
  display: block;
  width: 100%;
  border-radius: 5px;
  border: 0px;
  padding: 8px 0px;
  background-color: #ee6868;
  color: #fff;
  font-size: 1.3rem;
  outline: 0px;
  transition: all 0.2s ease-out;
  cursor: pointer;
  margin: 10px 0px;
}

.button.active,
.button:active,
.button:hover{
  background-color: #da5757;
  box-shadow: 0 0 0 0.3rem rgba(220,53,69,.5);
}
</style>
