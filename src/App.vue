<template>
  <div>
    <div class="page" v-bind:class="{ previewMode: previewMode }">
      <header id="header">
        <Topbar class="topbar"   v-on:preview="preview"/>
      </header>
      <main id="main">
        <ResumeEditor class="editor"/>
        <ResumePreview class="preview"/>
      </main>
      <button id="exitPreview" v-on:click="exitPreview">退出预览</button>
    </div>
  </div>
</template>

<script>
  import 'normalize.css/normalize.css'
  import './assets/reset.css'


  import Topbar from './components/Topbar'
  import ResumeEditor from './components/ResumeEditor'
  import ResumePreview from './components/ResumePreview'
  import icons from './assets/icons'
  import store from './store/index'

  import AV from './lib/leancloud'
  import getAVUser from './lib/getAVUser'

export default {
  data(){
    return {previewMode: false}
  },
  name: 'app',
  store,
  components: { Topbar, ResumeEditor, ResumePreview},
  created(){
    document.body.insertAdjacentHTML('afterbegin', icons)
    let state = localStorage.getItem('state')
    if(state){
      state = JSON.parse(state)
    }
    this.$store.commit('initState',state)
    this.$store.commit('setUser', getAVUser())
  },
  methods: {
    exitPreview(){
      this.previewMode = false
   },
    preview(){
      console.log("preview启动")
      this.previewMode = true
      console.log("wan")
    }
  }
}
</script>

<style lang="scss">
.page {
  height: 100vh;
  display: flex;
  flex-direction: column;
  background: #EAEBEC;
}
.page>main {
  flex-grow: 1;
}
.page>main {
  min-width: 1024px;
  max-width: 1440px;
  margin-top: 16px;
  margin-bottom: 16px;
  display: flex;
  justify-content: space-around;
  padding: 0 16px;
  width: 100%;
  align-self: center;
}
 #resumeEditor{
     min-width: 35%;
     background: #444;
   }
   #resumePreview{
     flex-grow: 1;
     margin-left: 16px;
     background: #777;
   }
   svg.icon {
    height: 1em;
    width: 1em;
    fill: currentColor;
    vertical-align: -0.1em;
    font-size: 16px;
   }
   .previewMode>#header{
     display: none;
   }
   .previewMode>#main>.editor{
     display: none;
   }
   .previewMode .preview{
     max-width: 800px;
     margin: 32px auto;
     overflow: none;
   }
   #exitPreview{
     display: none;
   }
   .previewMode #exitPreview{
     display: inline-block;
     position: fixed;
     right: 16px;
     top: 16px;
     height: 35px;
     border: none;
     width: 80px;
     background:#f6556c;
     cursor: pointer;
     border-radius: 3px;
     &:hover {
      box-shadow: 0 2px 3px 0 rgba(0,0,0,0.25);
     }
   }

</style>
