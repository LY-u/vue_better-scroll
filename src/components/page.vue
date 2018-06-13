<template>
  <div class="page">
    <scroll class="wrap"
            ref='scrollEle'
            :data="info"
            :pulldown="canPulldown"
            :pullup="canPullup"
            :listenScroll='true'
            :pullDownRefresh="pullDownRefreshObj"
            :pullUpLoad="pullUpLoadObj"
            @pulldown="loadData"
            @scrollToEnd='pullup'
            @scroll='scroll'>
      <div class="box" ref='box'>
        <div class="content" :style='`min-height:${mH}px`'>
          <div class="fresh"> loading...</div>
          <p class='li' v-for="item in info">{{item}}</p>
        </div>
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
      canPulldown:true,
      canPullup:true,
      msg: 'Welcome to Your Vue.js App',
      info:[
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome to Better-scroll',
        'Welcome t_o Better-scroll',
        'Welcome t_o Better-scroll',
        'Welcome t_o Better-scroll',
        'Welcome t_o Better-scroll',
        // 'Welcome t_o Better-scroll',
        // 'Welcome t_o Better-scroll',
        // 'Welcome to Better-scroll',
        // 'Welcome to Better-scroll',
        // 'Welcome to Better-scroll',
        // 'Welcome to Better-scroll',
        // 'Welcome t_o Better-scroll',
        // 'Welcome t_o Better-scroll',
        // 'Welcome t_o Better-scroll',
      ],
      mH:0,
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
    },
    pullUpLoadObj(){
      return {
        threshold: 60
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
    pullup(){
      console.log('pullup')
      setTimeout(()=>{
        this.info = this.info.concat(['123','87','45','456'])
        this.finishPullUp().then((res)=>{
          console.log('up - finish')
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
    finishPullUp() {
      return this.$refs.scrollEle.finishPullUp()
    },
    initScroll() {
      return this.$refs.scrollEle._initScroll()
    },
    refreshScroll() {
      return this.$refs.scrollEle.refresh()
    },
  },
  mounted(){
    
    this.mH = this.$refs.box.clientHeight + 1
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
.box{
  min-height: 100%;
}
.content{
  /*min-height: 800px;*/
}
.fresh{
  height: 50px;
  line-height: 50px;
  margin-top: -50px;
  text-align: center;
}
</style>
