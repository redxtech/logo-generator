<template>
  <div id="svg">
    <!--suppress CssUnknownProperty -->
    <svg
      version="1.1"
      id="Layer_1"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      x="0px"
      y="0px"
      viewBox="0 0 620 620"
      style="enable-background:new 0 0 620 620;"
      xml:space="preserve"
    >
      <!-- Outer and inner bounds of hexagon -->
      <polygon
        class="st0"
        points="51.6,156.4 51.6,463.7 310.1,617.4 568.5,463.7 568.5,156.4 310.1,2.8"
      />
      <polygon
        class="st0"
        points="144.7,211.8 144.7,408.5 310.1,506.8 475.4,408.5 475.4,211.8 310.1,113.5"
      />
      <!-- X in middle of hexagon -->
      <text
        transform="matrix(1 0 0 1 203.5 432.6)"
        class="st2"
      >
        X
      </text>
      <!--Segments to fill in hexagon-->
      <polygon
        class="seg0"
        points="310.1,2.8 568.5,156.4 475.4,211.8 310.1,113.5"
      />
      <polygon
        class="seg1"
        points="568.5,156.4 568.5,463.7 475.4,408.5 475.4,211.8"
      />
      <polygon
        class="seg2"
        points="568.5,463.7 310.1,617.4 310.1,506.8 475.4,408.5"
      />
      <polygon
        class="seg3"
        points="310.1,617.4 51.6,463.7 144.7,408.5 310.1,506.8"
      />
      <polygon
        class="seg4"
        points="51.6,463.7 51.6,156.4 144.7,211.8 144.7,408.5"
      />
      <polygon
        class="seg5"
        points="51.6,156.4 310.1,2.8 310.1,113.5 144.7,211.8"
      />
      <!-- Hexagon lines -->
      <line
        class="st1"
        x1="310.1"
        y1="2.8"
        x2="310.1"
        y2="113.5"
      />
      <line
        class="st1"
        x1="568.5"
        y1="156.4"
        x2="475.4"
        y2="211.8"
      />
      <line
        class="st1"
        x1="568.5"
        y1="463.7"
        x2="475.4"
        y2="408.5"
      />
      <line
        class="st1"
        x1="310.1"
        y1="617.4"
        x2="310.1"
        y2="506.8"
      />
      <line
        class="st1"
        x1="51.6"
        y1="463.7"
        x2="144.7"
        y2="408.5"
      />
      <line
        class="st1"
        x1="51.6"
        y1="156.4"
        x2="144.7"
        y2="211.8"
      />
    </svg>
  </div>
</template>

<script>
  export default {
    name: 'svg-generator',
    props: {
      xColour: {
        type: String,
        required: false,
        default: '#E31133'
      },
      segments: {
        type: Array,
        required: false,
        default: () => {
          return ['#009DE7', '#00A8F7']
        }
      },
      thickness: {
        type: Number,
        required: false,
        default: 1.5
      },
      lineThickness: {
        type: Number,
        required: false,
        default: 0.5
      }
    },
    date () {
      return {
        svg: undefined
      }
    },
    watch: {
      xColour (val) {
        this.svg.style.setProperty('--x-colour', val)
      },
      segments () {
        this.svg.style.setProperty(`--seg-0`, this.segments[0])
        this.svg.style.setProperty(`--seg-1`, this.segments[1])
      },
      thickness () {
        this.svg.style.setProperty(`--border-thickness`, this.thickness)
      },
      lineThickness () {
        this.svg.style.setProperty(`--line-thickness`, this.lineThickness)
      }
    },
    mounted () {
      const svg = window.document.querySelector('#svg')
      this.svg = svg
      svg.style.setProperty('--x-color', this.xColour)
      svg.style.setProperty(`--seg-0`, this.segments[0])
      svg.style.setProperty(`--seg-1`, this.segments[1])
      svg.style.setProperty(`--border-thickness`, this.thickness)
      svg.style.setProperty(`--line-thickness`, this.lineThickness)
    }
  }
</script>

<style>
  /* Import Exo 2 font */
  @import url('https://fonts.googleapis.com/css?family=Exo+2');

  /* Variables */
  #svg {
    --x-colour: #E31133;
    --seg-0: #009DE7;
    --seg-1: #00A8F7;
    --border-thickness: 1.5;
    --line-thickness: 0.0;

    margin: 1rem auto;
    max-width: 400px;
    max-height: 400px;
  }

  /* SVG Styling */
  .st0 {
    fill: #FFFFFF;
    stroke: #000000;
    stroke-width: var(--border-thickness);
    stroke-miterlimit: 10;
  }

  .st1 {
    fill: none;
    stroke: #000000;
    stroke-width: var(--line-thickness);
    stroke-miterlimit: 10;
  }

  .st2 {
    font-family: 'Exo 2', sans-serif;
    font-size: 354.591px;
    fill: var(--x-colour);
  }

  .seg0 {
    fill: var(--seg-0);
  }

  .seg1 {
    fill: var(--seg-1);
  }

  .seg2 {
    fill: var(--seg-0);
  }

  .seg3 {
    fill: var(--seg-1);
  }

  .seg4 {
    fill: var(--seg-0);
  }

  .seg5 {
    fill: var(--seg-1);
  }
</style>
