<template>
  <div class="page">
    <scroll class="wrap"
            ref='scrollEle'
            :data="info"
            :pulldown="true"
            :listenScroll='true'
            :pullDownRefresh="pullDownRefreshObj"
            @pulldown="loadData"
            @scroll='scroll'>
      <div class="content">
        <div class="fresh"> loading...</div>
        <p class='li' v-for="item in info">{{item}}</p>
        <p class='li to'>middle</p>
        <p class='li' v-for="item in info">{{item}}</p>
      </div>
    </scroll>
  </div>
</template>

<script>

import BScroll from 'better-scroll'
import scroll from './scroll'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      info:[
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
      ],
    }
  },
  components:{
    'scroll':scroll,
  },
  computed:{
    pullDownRefreshObj(){
      return {
        threshold: 60,
        stop: 50,
        stopTime:500
      }
    }
  },
  methods:{
    loadData(){
      console.log('pulldown')
      setTimeout(()=>{
        this.finishPullDown().then((res)=>{
          console.log('finish')
          setTimeout(()=>{
            this.refreshScroll()
          },700)
        })
        
      },1000)
    },
    scroll(pos){
      // console.log(pos.y)
    },
    scrollTo(y) {
      return new Promise((resolve)=>{
        this.$refs.scrollEle.scrollTo(0, -y, 500, 'bounce')
        resolve()
      })
    },
    scrollToElement(){
      let el = document.querySelector('.to')
      this.$refs.scrollEle.scrollToElement(el,700)
    },
    finishPullDown() {
      return this.$refs.scrollEle.finishPullDown()
    },
    initScroll() {
      return this.$refs.scrollEle._initScroll()
    },
    refreshScroll() {
      return this.$refs.scrollEle.refresh()
    },
  },
  mounted(){
    // 初始化
    this.initScroll()
  },
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html,body,#app,.page,.wrap{
  height: 100%;
}
.li{
  text-align: center;
  padding:18px;
}
.content{}
.fresh{
  height: 50px;
  line-height: 50px;
  margin-top: -50px;
  text-align: center;
}
</style>
