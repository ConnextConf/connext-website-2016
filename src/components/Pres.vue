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
      $(".footer").css("display", "none")
      $("body").css("overflow", "hidden")
      $(".circle-container").width($(".circle").length * $(window).height() * 0.01 * 30)
      function horizontalWheel(eve, el) {
        el.scrollLeft += (eve.deltaX !== undefined) ? eve.deltaX :
                        (eve.detail !== undefined && eve.detail !== 0) ? eve.detail :
                            -eve.wheelDelta;
        el.scrollLeft += (eve.deltaY !== undefined) ? eve.deltaY :
                        (eve.detail !== undefined && eve.detail !== 0) ? eve.detail :
                            -eve.wheelDelta;
      }
      $(window).bind("touchstart", touchStart);
      var start = {x:0,y:0};
      function touchStart(event) {
        start.x = event.originalEvent.touches[0].pageX;
        start.y = event.originalEvent.touches[0].pageY;
      }
      var wx = document.querySelector('body');
      $(window).bind("mousewheel DOMMouseScroll", function(event){
        event.preventDefault();
        horizontalWheel(event.originalEvent, wx);
        return false;})
      $(window).bind("touchmove", function(e){
        e.preventDefault();
        var offset = {};
        offset.deltaX = start.x - e.originalEvent.touches[0].pageX;
        offset.deltaY = start.y - e.originalEvent.touches[0].pageY;
        horizontalWheel(offset, wx);
        return false;
      })
    },
    resize() {
      $(".circle-container").width($(".circle").length * $(window).height() * 0.01 * 26)

    }
  }
</script>
<template lang="jade">
.container.pres
  .title
    .context
      h1 分享嘉宾
      p 这里是一串很长的文字
    p.arrow.shake-slow.shake-horizontal-slow.shake-horizontal.shake-constant.shake-constant--hover
      i(aria-hidden="true" class="fa fa-angle-double-right")
  .circle-container
    .circle
      .flipper
        .front
          .f
            h1 Linghein Mattrick
            p 吃喝嫖赌午餐券吃喝嫖赌午餐券吃喝嫖赌午餐券
        .back
          .b
            img.avatar(src="../avatars/linghein_ho.jpg")
            p
              a(href="#") 查看详情
    .circle
      .flipper
        .front
          .f
            h1 hello
            p hahahahah
        .back
          .b
            img.avatar(src="../avatars/linghein_ho.jpg")
            p
              a(href="#") 查看详情
    .circle
      .flipper
        .front
          .f
            h1 hello
            p hahahahah
        .back
          .b
            img.avatar(src="../avatars/linghein_ho.jpg")
            p
              a(href="#") 查看详情
    .circle
      .flipper
        .front
          .f
            h1 hello
            p hahahahah
        .back
          .b
            img.avatar(src="../avatars/linghein_ho.jpg")
            p
              a(href="#") 查看详情
</template>
<style lang="stylus">
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
  .title
    width 80vw
    height 100%
    position fixed
    left 0
    top 0
    background #546E7A
    color white
    display flex
    align-items center
    align-content center
    box-shadow 0 0 10px #404040 inset
    padding-left 3vw
    h1
      font-size 4.6vh
      line-height 4.3vh
      margin-bottom 4vh
      font-weight 300
    p
      color #fff
      line-height 2.2vh
      font-weight 300
      letter-spacing 0.2rem
    p.arrow
      position absolute
      top 50%
      left 72vw
  .circle-container
    width 100%
    height 100%
    background white
    left 80vw
    position absolute
    padding-left 10vw
    display flex
    align-items center
    top 0
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
      border 1px solid #00695C
      color #00695C
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