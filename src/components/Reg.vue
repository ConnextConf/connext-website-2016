<script>
  import under_cons from "./under_cons.vue"
  export default {
    name: "Reg",
    components: {
      under_cons
    }
  }
</script>
<template>
<div class="container reg">
  <div class="darken">
  </div>
  <div class="_slogan">
    <p class="title">在 Connext，<br>让更多人<br>听到你的声音。</p>
    <p>无论你是青少年项目的参与者、经验丰富的技术人员还是互联网领域关注者，<br>Connext 都可以为你提供分享、展示与交流的机会和舞台。</p>
    <p>我们欢迎热爱互联网的你，<br>以分享者身份参与 7 月的 meetup。</p>
    <p class="btn"><a href="http://form.mikecrm.com/p0Eaex" target="_blank"><i class="fa fa-angle-double-right" aria-hidden="true"></i> 讲者注册</a></p>
    <p class="notice">将跳转至讲者注册表单，请在表单中填写必要信息。<br>我们将会在三个工作日内联系你，请保持联系畅通。</p>
  </div>
</div>
</template>
<style lang="stylus">
.container.reg
  margin-top 0
  padding-bottom 10vh
  height 100vh
  width 100%
  background url("../backgrounds/1_a.jpg")
  background-size cover
  background-position center center
  .darken
  	position absolute
  	left 0
  	top 0
  	background rgba(0,0,0,.6)
  	width 100%
  	height 100%
  ._slogan
    font-size 2vh
    position absolute
    top 50%
    height 30%
    left 25%
    width 100%
    margin -15% 0 0 -25%
    bottom 10%
    padding 5vh 10vw 0 4vw
    .title
      font-size 4.6vh
      line-height 4.3vh
      margin-bottom 4vh
      font-size 700
  	p
   	  color white
   	  line-height 2.2vh
   	  font-weight 300
   	  letter-spacing 0.2rem
    .notice
      font-size 1.2vh
    .btn
      font-size 1.6vh
      background white
      border-radius 0
      padding 0.8rem 1.4rem !important
      margin-top 2vh
      margin-bottom 1vh
      a
        text-decoration none
        color #000 !important
        transition color 0.5s
        padding .6rem 1.4rem
        letter-spacing .4rem
      	&:hover
      	  color #229ebe !important
</style>