<script>
  export default {
    name: "Pres",
    methods: {
      getRandomSquare() {
        let a = Math.ceil(Math.random()*100)*3
        return "width:"+a+"px;height:"+a+"px;"
      }
    },
    ready() {
      let getRandomColor = function() {
        let h = Math.floor(Math.random()*(359-0+1)+0)
        let color = "hsla(" + h + ",49%,70%,0.7)"
        return color
      }
      $(".front").each(function(n, ele){
        $(ele).css("background", getRandomColor())
      })
      $(".footer").css("display", "none")
      $("body").css("overflow", "hidden")
      $(".circle-container").width($(".circle").length * $(window).height() * 0.01 * 26)
      function horizontalWheel(eve, el) {
        el.scrollLeft += (eve.deltaX !== undefined) ? eve.deltaX :
                        (eve.detail !== undefined && eve.detail !== 0) ? eve.detail :
                            -eve.wheelDelta
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
        a 按照您的使用习惯滑动页面

  .circle-container
    .blur
    .circle
      .flipper
        .front
          .f
            h1 王鹏翰 / wph95
            p
              | CodeVS.cn
              br
              | 创始人
        .back
          .b
            img.avatar(src="../speakers/penghan_wang.jpg")

    .circle
      .flipper
        .front
          .f
            h1 高阳 / Sunny
            p SegmentFault CEO
        .back
          .b
            img.avatar(src="../speakers/sunny_gao.png")

    .circle
      .flipper
        .front
          .f
            h1 赵坤安 / undownding
            p Ezbuy.com Android 架构师
        .back
          .b
            img.avatar(src="../speakers/kunan_zhao.jpg")

    .circle
      .flipper
        .front
          .f
            h1 王天宇 / Cee Cirno
            p iOS 开发者
        .back
          .b
            img.avatar(src="../speakers/cee_cirno.png")

    .circle
      .flipper
        .front
          .f
            h1 朱锦涛 / Clerk Zhu
            p CorpsX 联合创始人
        .back
          .b
            img.avatar(src="../speakers/clerk_zhu.png")

    .circle
      .flipper
        .front
          .f
            h1 刘恩泽 / Micromacer
            p 青少年 UI 设计师
        .back
          .b
            img.avatar(src="../speakers/penghan_wang.jpg")

    .circle
      .flipper
        .front
          .f
            h1 王逸翛 / Tex Wang
            p
              |风暴云文档创始人
              br
              |休学创业者
        .back
          .b
            img.avatar(src="../speakers/tex_wang.png")

    .circle
      .flipper
        .front
          .f
            h1 徐浩继 / Altoria
            p 青少年个人开发者
        .back
          .b
            img.avatar(src="../speakers/penghan_wang.jpg")

    .circle
      .flipper
        .front
          .f
            h1 徐闻康 / Weny
            p ForK12 教育基础接入平台开发者
        .back
          .b
            img.avatar(src="../speakers/wk_x.jpg")

    .circle
      .flipper
        .front
          .f
            h1 吴子谦
            p 青少年创客
        .back
          .b
            img.avatar(src="../speakers/ziqian_wu.jpg")

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
    background-image url("../backgrounds/1_a.jpg")
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