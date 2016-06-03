<script>
  export default {
    name: "Pres",
    methods: {
      scrollToContent() {
       $('html,body').animate({scrollLeft:$('.title').width()}, 1000);
      },
      getRandomColor() {
        let h = Math.floor(Math.random()*(359-0+1)+0)
        let color = "hsla(" + h + ",49%,70%,0.7)"
        return color
      }
    },
    ready() {
      $(".footer").css("display", "none")
      $("body").css("overflow", "hidden")
      $(".circle-container").width($(".circle").length * $(window).height() * 0.01 * 26)
      function horizontalWheel(eve, el) {
        el.scrollLeft += (eve.deltaY !== undefined) ? eve.deltaY :
                        (eve.detail !== undefined && eve.detail !== 0) ? eve.detail :
                            -eve.wheelDelta
      }
      $(window).bind("touchstart", touchStart)
      var start = {x:0,y:0}
      function touchStart(event) {
        start.x = event.originalEvent.touches[0].pageX
        start.y = event.originalEvent.touches[0].pageY
      }
      var wx = document.querySelector('body')
      $(window).bind("mousewheel DOMMouseScroll", function(event){
        event.preventDefault()
        horizontalWheel(event.originalEvent, wx)
        return false
      })
      $(window).bind("touchmove", function(e){
        e.preventDefault();
        var offset = {}
        offset.deltaX = start.x - e.originalEvent.touches[0].pageX
        offset.deltaY = start.y - e.originalEvent.touches[0].pageY
        horizontalWheel(offset, wx)
        return false
      })
    },
    data() {
      return {
        "speakers": [
          {
          "name": "王鹏翰 / wph95",
          "discription": "CodeVS.cn<br>创始人",
          "image": require("../speakers/penghan_wang.jpg")
          },
          {
          "name": "高阳 / Sunny",
          "discription": "SegmentFault CEO",
          "image": require("../speakers/sunny_gao.png")
          },
          {
          "name": "赵坤安 / undownding",
          "discription": "Ezbuy.com Android 架构师",
          "image": require("../speakers/kunan_zhao.jpg")
          },
          {
          "name": "王天宇 / Cee Cirno",
          "discription": "iOS 开发者",
          "image": require("../speakers/cee_cirno.png")
          },
          {
          "name": "朱锦涛 / Clerk Zhu",
          "discription": "CorpsX 联合创始人",
          "image": require("../speakers/clerk_zhu.png")
          },
          {
          "name": "刘恩泽 / Micromacer",
          "discription": "青少年 UI 设计师",
          "image": require("../speakers/enze_liu.jpg")
          },
          {
          "name": "王逸翛 / Tex Wang",
          "discription": "风暴云文档创始人<br>休学创业者",
          "image": require("../speakers/tex_wang.png")
          },
          {
          "name": "徐浩继 / Altoria",
          "discription": "青少年个人开发者",
          "image": require("../speakers/altoria.jpg")
          },
          {
          "name": "徐闻康 / Weny",
          "discription": "ForK12 教育基础接入平台开发者",
          "image": require("../speakers/wk_x.jpg")
          },
          {
          "name": "吴子谦",
          "discription": "青少年创客",
          "image": require("../speakers/ziqian_wu.jpg")
          }
        ]
      }
    },
    resize() {
      $(".circle-container").width($(".circle").length * $(window).height() * 0.01 * 26)

    }
  }
</script>
<template lang="jade">
.background
.container.pres
  .title
    .context
      h1 分享嘉宾
      p 「行业嘉宾、同龄人和他们的澎湃之声」
      p
        a(v-on:click="scrollToContent()") 请上下滑动页面

  .circle-container
    .blur
    .circle(v-for="s in speakers")
      .flipper
        .front(:style="'background:' + getRandomColor()")
          .f
            h1 {{ s.name }}
            p {{{ s.discription }}}
        .back
          .b
            img.avatar(:src="s.image")

</template>
<style lang="stylus" scoped>
body

.shake-slow.shake-horizontal
  animation-duration 10s !important
  animation-iteration-count infinite
  animation-name shake-horizontal
  animation-timing-function ease-in-out
.container.pres
  margin-top 0
  padding-top 50px
  height 100vh
  width 100vw
  background-image url("../backgrounds/tianyu.jpg")
  background-size cover
  background-position 10% center
  .title
    width 80vw
    height 100%
    position absolute
    left 0
    top 0
    background rgba(0, 0, 0, 0.85)
    color white
    display flex
    align-items center
    align-content center
    transition all .3s
    &:hover
      background rgba(0, 0, 0, 0.55)
    .context
      text-align center
      width 100%
    h1
      font-size 4.6vh
      line-height 4.3vh
      margin-bottom 4vh
      font-weight 300
    p
      color #fff
      line-height 3.2vh
      font-weight 300
      width 80%
      margin auto
      letter-spacing 0.2rem
      &:nth-child(odd)
        position absolute
        bottom 15vh
        left 0
        width 100%
      a
        color white
        border-radius 3px
        border 1px solid white
        padding .5rem 1.5rem
        margin-top 1rem
        font-size xx-small
    p.arrow
      position absolute
      top 50%
      left 72vw
  .circle-container
    width 100%
    height 100%
    left 80vw
    position absolute
    padding-left 10vw
    display flex
    align-items center
    top 0
    background-image url("../backgrounds/tianyux.jpg")
    background-size cover
    background-position 10% center
    transition all .3s
    &:hover
      .blur
        background rgba(0,0,0,.65)
    .blur
      position absolute
      left 0
      top 0
      width 100%
      height 100%
      background rgba(0,0,0,.85)
      transition all .3s
    .circle {
      perspective 1000
    }
      /* flip the pane when hovered */
    .circle:hover .flipper, .circle.hover .flipper {
      transform rotateY(180deg)
    }

    .circle, .front, .back {
      width 25vh
      height 25vh
    }

    /* flip speed goes here */
    .flipper {
      transition 0.6s
      transform-style preserve-3d
      position relative
    }

    /* hide back of pane during swap */
    .front, .back
      backface-visibility hidden
      display flex
      align-content center
      align-items center
      justify-content center
      position absolute
      top 0
      left 0
      background rgba(255,255,255,.6)
      border-radius 100%
      h1
        font-size 2.6vh
        line-height 1vh
        font-weight 100
        text-align center
      p
        font-size 1.8vh
        font-weight 100
        text-align center
        max-width 20vh
        margin auto
    /* front pane, placed above back */
    .front {
      z-index 2
    }

    /* back, initially hidden pane */
    .back
      transform rotateY(180deg)
      .b
        height 25vh
        width 25vh
        .avatar
          position absolute
          width: 25vh;
          height: 25vh;
        p
          position: relative;
          font-size: 3.4vh;
          height: 25vh;
          max-width 25vh !important
          line-height: 25vh;
          background: rgba(0, 0, 0, 0.45);
          border-radius: 100vh;
          a
            color white
    .circle
      height 25vh
      width 25vh
      margin 0
      border-radius 100vmax
      color white
      img
        width 100%
        border-radius 100vh
      &:nth-child(odd)
        align-self center
        transform translateY(15vh)
      &:nth-child(even)
        align-self center
        transform translateY(-10vh)

</style>