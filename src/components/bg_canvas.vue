<script>
  export default {
    name: "bg_canvas",
    ready: function(){
        var h = screen.height;
  var w = screen.width;
  var canvas = document.getElementById('bg_canvas'),
  context = canvas.getContext('2d'),
  particles = [],
  numParticles = 15,
  minDist = 100,
  springAmount = 0.0000005;
  canvas.setAttribute('width', w);
  canvas.setAttribute('height', h);
  for (var size, particle, i = 0; i < numParticles; i++) {
    size = Math.random() * 10 + 2;
    particle = new Ball(size, "#d4d4d4");
    particle.x = Math.random() * canvas.width;
    particle.y = Math.random() * canvas.height;
    particle.vx = Math.random() * 6 - 3;
    particle.vy = Math.random() * 6 - 3;
    particle.mass = size;
    particles.push(particle);
  }
function spring(partA, partB) {
    var dx = partB.x - partA.x,
    dy = partB.y - partA.y,
    dist = Math.sqrt(dx * dx + dy * dy);

    if (dist < minDist) {
      var alpha = 1 - dist / minDist;
      context.strokeStyle = utils.colorToRGB("#aaaaaa", alpha);
      context.beginPath();
      context.moveTo(partA.x, partA.y);
      context.lineTo(partB.x, partB.y);
      context.stroke();

      var ax = dx * springAmount,
      ay = dy * springAmount;
      partA.vx += ax / partA.mass;
      partA.vy += ay / partA.mass;
      partB.vx -= ax / partB.mass;
      partB.vy -= ay / partB.mass;
    }
  }
function move(partA, i) {
    partA.x += partA.vx;
    partA.y += partA.vy;
    if (partA.x > canvas.width) {
      partA.x = 0;
    } else if (partA.x < 0) {
      partA.x = canvas.width;
    }
    if (partA.y > canvas.height) {
      partA.y = 0;
    } else if (partA.y < 0) {
      partA.y = canvas.height;
    }
    for (var partB, j = i + 1; j < numParticles; j++) {
      partB = particles[j];
      spring(partA, partB);
    }
}
function draw(particle) {
    particle.draw(context);
  }

  (function drawFrame() {
    window.requestAnimationFrame(drawFrame, canvas);
    context.clearRect(0, 0, canvas.width, canvas.height);

    particles.forEach(move);
    particles.forEach(draw);
  } ());
    }
  }
if (!window.requestAnimationFrame) {
  window.requestAnimationFrame = (window.webkitRequestAnimationFrame ||
                                  window.mozRequestAnimationFrame ||
                                  window.msRequestAnimationFrame ||
                                  window.oRequestAnimationFrame ||
                                  function (callback) {
                                    return window.setTimeout(callback, 17 /*~ 1000/60*/);
                                  });
}
if (!window.cancelRequestAnimationFrame) {
  window.cancelRequestAnimationFrame = (window.cancelAnimationFrame ||
                                        window.webkitCancelRequestAnimationFrame ||
                                        window.mozCancelRequestAnimationFrame ||
                                        window.msCancelRequestAnimationFrame ||
                                        window.oCancelRequestAnimationFrame ||
                                        window.clearTimeout);
}
window.utils = {};
window.utils.captureMouse = function (element) {
var mouse = {x: 0, y: 0, event: null},
      body_scrollLeft = document.body.scrollLeft,
      element_scrollLeft = document.documentElement.scrollLeft,
      body_scrollTop = document.body.scrollTop,
      element_scrollTop = document.documentElement.scrollTop,
      offsetLeft = element.offsetLeft,
      offsetTop = element.offsetTop;
element.addEventListener('mousemove', function (event) {
    var x, y;
    if (event.pageX || event.pageY) {
      x = event.pageX;
      y = event.pageY;
    } else {
      x = event.clientX + body_scrollLeft + element_scrollLeft;
      y = event.clientY + body_scrollTop + element_scrollTop;
    }
    x -= offsetLeft;
    y -= offsetTop;
    mouse.x = x;
    mouse.y = y;
    mouse.event = event;
  }, false);
  return mouse;
};
window.utils.captureTouch = function (element) {
  var touch = {x: null, y: null, isPressed: false, event: null},
      body_scrollLeft = document.body.scrollLeft,
      element_scrollLeft = document.documentElement.scrollLeft,
      body_scrollTop = document.body.scrollTop,
      element_scrollTop = document.documentElement.scrollTop,
      offsetLeft = element.offsetLeft,
      offsetTop = element.offsetTop;
  element.addEventListener('touchstart', function (event) {
    touch.isPressed = true;
    touch.event = event;
  }, false);
  element.addEventListener('touchend', function (event) {
    touch.isPressed = false;
    touch.x = null;
    touch.y = null;
    touch.event = event;
  }, false);
  element.addEventListener('touchmove', function (event) {
    var x, y,
        touch_event = event.touches[0]; //first touch
    if (touch_event.pageX || touch_event.pageY) {
      x = touch_event.pageX;
      y = touch_event.pageY;
    } else {
      x = touch_event.clientX + body_scrollLeft + element_scrollLeft;
      y = touch_event.clientY + body_scrollTop + element_scrollTop;
    }
    x -= offsetLeft;
    y -= offsetTop;
    touch.x = x;
    touch.y = y;
    touch.event = event;
  }, false);
  return touch;
};
window.utils.parseColor = function (color, toNumber) {
  if (toNumber === true) {
    if (typeof color === 'number') {
      return (color | 0); //chop off decimal
    }
    if (typeof color === 'string' && color[0] === '#') {
      color = color.slice(1);
    }
    return window.parseInt(color, 16);
  } else {
    if (typeof color === 'number') {
      color = '#' + ('00000' + (color | 0).toString(16)).substr(-6); //pad
    }
    return color;
  }
};
window.utils.colorToRGB = function (color, alpha) {
  // http://www.codefans.net
  if (typeof color === 'string' && color[0] === '#') {
    color = window.parseInt(color.slice(1), 16);
  }
  alpha = (alpha === undefined) ? 1 : alpha;
  //parse hex values
  var r = color >> 16 & 0xff,
      g = color >> 8 & 0xff,
      b = color & 0xff,
      a = (alpha < 0) ? 0 : ((alpha > 1) ? 1 : alpha);
  //only use 'rgba' if needed
  if (a === 1) {
    return "rgb("+ r +","+ g +","+ b +")";
  } else {
    return "rgba("+ r +","+ g +","+ b +","+ a +")";
  }
};
window.utils.containsPoint = function (rect, x, y) {
  return !(x < rect.x ||
           x > rect.x + rect.width ||
           y < rect.y ||
           y > rect.y + rect.height);
};
window.utils.intersects = function (rectA, rectB) {
  return !(rectA.x + rectA.width < rectB.x ||
           rectB.x + rectB.width < rectA.x ||
           rectA.y + rectA.height < rectB.y ||
           rectB.y + rectB.height < rectA.y);
};
//###[ball.js]###
function Ball (radius, color) {
  if (radius === undefined) { radius = 80; }
  if (color === undefined) { color = "#555"; }
  this.x = 0;
  this.y = 0;
  this.radius = radius;
  this.vx = 0;
  this.vy = 0;
  this.rotation = 0;
  this.scaleX = 1;
  this.scaleY = 1;
  this.color = utils.parseColor(color);
  this.lineWidth = 1;
}
Ball.prototype.draw = function (context) {
  context.save();
  context.translate(this.x, this.y);
  context.rotate(this.rotation);
  context.scale(this.scaleX, this.scaleY);
  context.lineWidth = this.lineWidth;
  context.fillStyle = this.color;
  context.beginPath();
  //x, y, radius, start_angle, end_angle, anti-clockwise
  context.arc(0, 0, this.radius, 0, (Math.PI * 2), true);
  context.closePath();
  context.fill();
  if (this.lineWidth > 0) {
    context.stroke();
  }
  context.restore();
};

Ball.prototype.getBounds = function () {
  return {
    x: this.x - this.radius,
    y: this.y - this.radius,
    width: this.radius * 2,
    height: this.radius * 2
  };
};
window.onload = function() {

};
</script>

<template>
  <canvas id="bg_canvas"></canvas>
</template>

<style>
@keyframes fadeIn_bg {
  0% {
    opacity: 0;
  }
  100% {
    opacity: .8;
  }
}
#bg_canvas {
  filter: blur(3px);
  opacity: .8;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 0;
  animation-name: fadeIn;
  animation-duration: 2s;
  animation-timing-function: ease-in;
  animation-iteration-count: 1;
  animation-delay: 0s;
}
</style>
