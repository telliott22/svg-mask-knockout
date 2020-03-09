<template>
  <main
    class="page"
    :class="{'page--game-finished' :gameFinished}"
  >

    <div
      class="page__background-container"
      id="background"
    >

      <div class="page__svg-container">

        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="100%"
          width="100%"
          id="rootSvg"
        >

          <defs>
            <mask
              id="mask"
              x="0"
              y="0"
              height="100%"
              width="100%"
            >
              <rect
                x="0"
                y="0"
                fill="#fff"
              />

              <circle
                id="circle"
                alignment-baseline="center"
                :style="circleStyles"
              />

              <g
                height="100%"
                x="0"
                y="0"
                id="headerText"
              >
                <text
                  x="0"
                  y="0"
                  fill="#000"
                >{{headerText}}</text>

              </g>

              <text
                x="0"
                y="0"
                fill="#000"
                id="countdown"
              >02:00</text>

            </mask>
          </defs>

          <rect
            x="0"
            y="0"
            mask="url(#mask)"
            fill="#000"
          />
        </svg>

      </div>
    </div>

  </main>
</template>

<script>
import anime from "animejs/lib/anime.es.js";

export default {
  data() {
    return {
      timeline: null,
      headerText: "Where's wally?",
      transformX: 50,
      transformY: 50,
      targetX: 564,
      targetY: 1406,
      //Sarcastic squidward
      // targetX: 1094,
      // targetY: 1298,
      range: 50,
      countdown: "01:00",
      timerInterval: null,
      circleRadius: 190,
      canvas1: null,
      canvas2: null,
      gameFinished: false
    };
  },
  computed: {
    circleStyles() {
      return {
        transform:
          "translateX(" +
          this.transformX +
          "%" +
          ") translateY(" +
          this.transformY +
          "%" +
          ")"
      };
    }
  },
  watch: {
    countdown(newVal) {
      if (newVal === "00:00") {
        alert("OVER");
        this.stopTimer();
      }
    }
  },
  methods: {
    onclick(e) {
      let background = document.getElementById("background");

      let backgroundElement = background.getBoundingClientRect();
      let clickX = e.clientX - backgroundElement.left;
      let clickY = e.clientY - backgroundElement.top;

      console.log("clickX", clickX);
      console.log("clickY", clickY);

      if (
        clickX > this.targetX - this.range &&
        clickX < this.targetX + this.range &&
        clickY > this.targetY - this.range &&
        clickY < this.targetY + this.range
      ) {
        this.successMessage();
      }
    },
    successMessage() {
      this.stopTimer();

      this.gameFinished = true;

      document.onmousemove = null;

      let circle = document.getElementById("circle");

      this.triggerConfetti();

      anime({
        targets: circle,
        r: this.circleRadius,
        easing: "easeInOutQuad",
        duration: 500,
        complete: anim => {
          //fire confetti
          // $this.startTimer(60);
        }
      });
    },
    onmousemove(e) {
      this.cursorLocation = { x: e.clientX, y: e.clientY };

      let viewportHeight = document.documentElement.clientHeight;
      let viewportWidth = document.documentElement.clientWidth;

      this.transformX = (this.cursorLocation.x / viewportWidth) * 100;
      this.transformY = (this.cursorLocation.y / viewportHeight) * 100;
    },
    startTimer(duration, display) {
      var timer = duration,
        minutes,
        seconds;

      let $this = this;
      let countdownElement = document.getElementById("countdown");

      this.timerInterval = setInterval(function() {
        minutes = parseInt(timer / 60, 10);
        seconds = parseInt(timer % 60, 10);

        minutes = minutes < 10 ? "0" + minutes : minutes;
        seconds = seconds < 10 ? "0" + seconds : seconds;

        $this.countdown = minutes + ":" + seconds;

        countdownElement.textContent = $this.countdown;

        if (--timer < 0) {
          timer = duration;
        }
      }, 1000);
    },
    stopTimer() {
      clearInterval(this.timerInterval);
    },
    initSVG() {
      let circle = document.getElementById("circle");
      let countdown = document.getElementById("countdown");

      //Wrap each header letter in a tspan
      let headerText = document.querySelector("#headerText text");

      headerText.innerHTML = headerText.textContent.replace(
        /\S/g,
        "<tspan class='letter'>$&</tspan>"
      );

      let headerTextLetters = document.querySelectorAll(".letter");

      //Init timeline
      this.timeline = anime.timeline({ autoplay: true });

      let $this = this;

      this.timeline
        .add({
          targets: headerTextLetters,
          opacity: [0, 1],
          easing: "easeInOutQuad",
          delay: anime.stagger(100),
          duration: 500
        })
        .add({
          targets: circle,
          transformX: [0, "50%"],
          transformY: [0, "50%"],
          easing: "easeInOutQuad",
          duration: 1000
        })
        .add({
          targets: circle,
          r: [0, this.circleRadius],
          easing: "easeInOutQuad",
          duration: 1000
        })
        .add({
          targets: circle,
          r: [this.circleRadius, this.circleRadius / 2],
          easing: "easeInOutQuad",
          duration: 1000,
          complete: anim => {
            document.onmousemove = this.onmousemove;
            document.ontouchmove = this.onmousemove;

            $this.startTimer(120);
          }
        })
        .add({
          targets: countdown,
          opacity: [0, 1],
          easing: "easeInOutBounce",
          duration: 500,
          delay: "+500"
        });
    },
    triggerConfetti() {
      const confetti = require("canvas-confetti");

      this.canvas1 = confetti.create(null, {
        resize: true
      });

      this.canvas2 = confetti.create(null, {
        resize: true
      });

      this.fireConfetti();
    },
    fireConfetti() {
      if (process.client) {
        let colors = [
          "#ffffff",
          "#00ccbb",
          "#4050fb",
          "#fb5058",
          "#ff9700",
          "#440063",
          "#fabe00"
        ];

        const shuffledColors = colors.sort(() => 0.5 - Math.random());

        this.canvas1({
          particleCount: 2,
          angle: 120,
          spread: 55,
          zIndex: 20000,
          origin: {
            x: 1,
            y: 1
          },
          colors: shuffledColors
        });

        this.canvas2({
          particleCount: 2,
          angle: 60,
          spread: 55,
          zIndex: 20000,
          origin: {
            x: 0,
            y: 1
          },
          colors: shuffledColors
        });

        if (!this.confettiTimer) {
          this.confettiTimer = Date.now() + 600;
        }

        if (Date.now() < this.confettiTimer) {
          requestAnimationFrame(this.fireConfetti);
        }
      }
    }
  },
  mounted() {
    document.onclick = this.onclick;

    this.initSVG();
  }
};
</script>
