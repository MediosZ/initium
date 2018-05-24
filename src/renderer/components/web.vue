<template lang="pug">
  #main
    .header
      img.btn(src="../../../static/back.png", @click="goBack()")
      img.btn(src="../../../static/forward.png", @click="goForward")
      img.btn(src="../../../static/fresh.png", @click="reload()")
      p.current-url {{url}}
    .loading
      p(v-show="!ready").text The initium is loading.
      <div v-show="!ready" class="loader" title="2">
        <svg version="1.1" id="loader-1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="100px" height="100px" viewBox="0 0 50 50" style="enable-background:new 0 0 50 50;" xml:space="preserve">
        <path fill="#888" d="M43.935,25.145c0-10.318-8.364-18.683-18.683-18.683c-10.318,0-18.683,8.365-18.683,18.683h4.068c0-8.071,6.543-14.615,14.615-14.615c8.072,0,14.615,6.543,14.615,14.615H43.935z">
        <animateTransform attributeType="xml" attributeName="transform" type="rotate" from="0 25 25"  to="360 25 25" dur="0.6s" repeatCount="indefinite"/>
        </path>
        </svg>
      </div>

    .content
      webview(src="http://www.theinitium.com" allowpopups).webview

</template>

<script>
  export default {
    name: 'main-page',
    data(){
      return {
        ready: false,
        webview: '',
        url: 'https://is loading'
      }
    },
    mounted(){
      const webview = document.querySelector('webview')
      webview.addEventListener('dom-ready', () => {
        this.ready = true
        this.url = webview.getURL()
      })

    },
    methods: {
      goBack(){
        const webview = document.querySelector('webview')
        webview.goBack()
      },
      goForward(){
        const webview = document.querySelector('webview')
        webview.goForward()
      },
      reload(){
        const webview = document.querySelector('webview')
        webview.reload()
      }
    }
  }
</script>

<style lang="stylus">
  #main
    width 100%
    height 100%

    .loading
      display flex
      flex-direction column
      justify-content center
      align-items center
      .text
        color #888
        font-size 100px
        margin 0 auto
      .loader
        width 100px
        height 100px

    .header
      display flex
      padding 3px 15px
      background-color #eee
      justify-content flex-start
      align-items center
      .btn
        margin 5px
        width 28px
        height 28px
      .current-url
        color black
        font-size 20px
        margin-left 20px
    .content
      width 100%
      height 100%
      .webview
        width 100%
        height 100%
</style>
