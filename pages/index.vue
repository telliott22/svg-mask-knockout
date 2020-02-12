<template>
  <main class="page">

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

            <svg>

              <g id="textPath">

                <path
                  id="curve"
                  d="M.314 212.744C-117.214 212.744-212.587 117.371-212.587-.157S-117.214-213.059.314-213.059 213.216-117.685 213.216-.157 117.842 212.744.314 212.744Z"
                  class="transparent"
                />
                <text>
                  <textPath
                    alignment-baseline="top"
                    xlink:href="#curve"
                  >
                    Working at DarkBlue in Shoreditch
                  </textPath>
                </text>

              </g>

            </svg>

            <circle
              id="circle"
              alignment-baseline="center"
            />

            <g
              height="100%"
              x="0"
              y="0"
              class="text-container"
            >
              <text
                x="0"
                y="0"
                fill="#000"
              >Excepteur sint</text>
              <text
                x="0"
                y="55"
                fill="#000"
              >cupidatat laborum</text>

            </g>

            <g
              height="100%"
              x="0"
              y="0"
              id="bottomRightText"
            >

              <svg
                xmlns:svg="http://www.w3.org/2000/svg"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 300 300"
                version="1.0"
                width="300"
                height="200"
                id="barcode"
              >
                <defs id="defs4" />
                <g
                  transform="translate(-319.65842,411.94414)"
                  id="layer1"
                >
                  <g
                    transform="matrix(11.791045,0,0,11.791045,2942.2704,3871.1998)"
                    id="barcode0"
                    style="fill:#000000"
                  >
                    <rect
                      width="1"
                      height="38"
                      x="-222"
                      y="-363"
                      id="barcode0_bar1"
                    />
                    <rect
                      width="1"
                      height="38"
                      x="-220"
                      y="-363"
                      id="barcode0_bar3"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-218"
                      y="-363"
                      id="barcode0_bar5"
                    />
                    <rect
                      width="4"
                      height="30"
                      x="-216"
                      y="-363"
                      id="barcode0_bar7"
                    />
                    <rect
                      width="2"
                      height="30"
                      x="-211"
                      y="-363"
                      id="barcode0_bar9"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-206"
                      y="-363"
                      id="barcode0_bar11"
                    />
                    <rect
                      width="2"
                      height="30"
                      x="-204"
                      y="-363"
                      id="barcode0_bar13"
                    />
                    <rect
                      width="3"
                      height="30"
                      x="-201"
                      y="-363"
                      id="barcode0_bar15"
                    />
                    <rect
                      width="4"
                      height="30"
                      x="-197"
                      y="-363"
                      id="barcode0_bar17"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-192"
                      y="-363"
                      id="barcode0_bar19"
                    />
                    <rect
                      width="1"
                      height="38"
                      x="-190"
                      y="-363"
                      id="barcode0_bar21"
                    />
                    <rect
                      width="1"
                      height="38"
                      x="-188"
                      y="-363"
                      id="barcode0_bar23"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-186"
                      y="-363"
                      id="barcode0_bar25"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-181"
                      y="-363"
                      id="barcode0_bar27"
                    />
                    <rect
                      width="2"
                      height="30"
                      x="-179"
                      y="-363"
                      id="barcode0_bar29"
                    />
                    <rect
                      width="2"
                      height="30"
                      x="-176"
                      y="-363"
                      id="barcode0_bar31"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-172"
                      y="-363"
                      id="barcode0_bar33"
                    />
                    <rect
                      width="3"
                      height="30"
                      x="-169"
                      y="-363"
                      id="barcode0_bar35"
                    />
                    <rect
                      width="1"
                      height="30"
                      x="-165"
                      y="-363"
                      id="barcode0_bar37"
                    />
                    <rect
                      width="3"
                      height="30"
                      x="-163"
                      y="-363"
                      id="barcode0_bar39"
                    />
                    <rect
                      width="1"
                      height="38"
                      x="-158"
                      y="-363"
                      id="barcode0_bar41"
                    />
                    <rect
                      width="1"
                      height="38"
                      x="-156"
                      y="-363"
                      id="barcode0_bar43"
                    />
                  </g>
                </g>
              </svg>

            </g>

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

  </main>
</template>

<script>
import anime from "animejs/lib/anime.es.js";

export default {
  methods: {},
  mounted() {
    let circle = document.getElementById("circle");
    let pathText = document.getElementById("textPath");

    let timeline = anime.timeline({ loop: true, autoplay: true });

    let circleRadius = 190;

    let circleBBox = circle.getBBox();
    timeline
      .add({
        targets: circle,
        r: [0, circleRadius],
        easing: "easeInOutQuad",
        duration: 1000,
        complete: function(anim) {
          // circleBBox = circle.getBBox();
        }
      })
      .add({
        targets: circle,
        r: [circleRadius, 0],
        easing: "easeInOutQuad",
        duration: 1000,
        delay: 1000
      });

    let pathTextTimeline = anime.timeline({ loop: true, autoplay: true });

    console.log(pathText);
    pathTextTimeline.add({
      targets: pathText,
      rotate: 360,
      easing: "linear",
      duration: 10000
    });
    // .add({
    //   targets: pathText,
    //   scale: ,
    //   easing: "easeInOutQuad",
    //   duration: 1000
    // });
  }
};
</script>
