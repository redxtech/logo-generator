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
      viewBox="0 0 1080 824"
      style="enable-background:new 0 0 1280 1024;"
      xml:space="preserve"
    >
      <!-- Outer and inner bounds of hexagon -->
      <polygon
        class="st0"
        points="381.9,302.3 381.9,609.6 640.4,763.3 898.8,609.6 898.8,302.3 640.4,148.7 "
      />
      <polygon
        class="st0"
        points="475,357.7 475,554.4 640.4,652.7 805.7,554.4 805.7,357.7 640.4,259.4 "
      />
      <!-- Hexagon lines -->
      <line
        class="st1"
        x1="640.4"
        y1="148.7"
        x2="640.4"
        y2="259.4"
      />
      <line
        class="st1"
        x1="805.7"
        y1="357.7"
        x2="898.8"
        y2="302.3"
      />
      <line
        class="st1"
        x1="805.7"
        y1="554.4"
        x2="898.8"
        y2="609.6"
      />
      <line
        class="st1"
        x1="640.4"
        y1="652.7"
        x2="640.4"
        y2="763.3"
      />
      <line
        class="st1"
        x1="475"
        y1="554.4"
        x2="381.9"
        y2="609.6"
      />
      <line
        class="st1"
        x1="381.9"
        y1="302.3"
        x2="475"
        y2="357.7"
      />
      <!-- X in middle of hexagon -->
      <text
        transform="matrix(1 0 0 1 533.2753 578.3199)"
        class="st2"
      >
        X
      </text>
      <!--Segments to fill in hexagon-->
      <polygon
        class="seg0"
        points="640.4,148.7 898.8,302.3 805.7,357.7 640.4,259.4"
      />
      <polygon
        class="seg1"
        points="898.8,302.3 898.8,609.6 805.7,554.4 805.7,357.7"
      />
      <polygon
        class="seg2"
        points="898.8,609.6 640.4,763.3 640.4,652.7 805.7,554.4"
      />
      <polygon
        class="seg3"
        points="640.4,763.3 381.9,609.6 475,554.4 640.4,652.7"
      />
      <polygon
        class="seg4"
        points="381.9,609.6 381.9,302.3 475,357.7 475,554.4"
      />
      <polygon
        class="seg5"
        points="381.9,302.3 640.4,148.7 640.4,259.4 475,357.7"
      />
    </svg>
  </div>
</template>

<script>
  export default {
    name: 'svg-generator',
    props: {
      xFont: {
        type: String,
        required: false,
        default: 'Exo 2'
      },
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
      }
    },
    date () {
      return {
        svg: undefined
      }
    },
    computed: {
      font () {
        return `'${this.xFont}'`
      }
    },
    watch: {
      xFont () {
        this.svg.style.setProperty('--x-font', this.font)
      },
      xColour (val) {
        this.svg.style.setProperty('--x-colour', val)
      },
      segments () {
        this.svg.style.setProperty(`--seg-0`, this.segments[0])
        this.svg.style.setProperty(`--seg-1`, this.segments[1])
      }
    },
    mounted () {
      const svg = window.document.querySelector('#svg')
      this.svg = svg
      svg.style.setProperty('--x-font', this.font)
      svg.style.setProperty('--x-color', this.xColour)
      svg.style.setProperty(`--seg-0`, this.segments[0])
      svg.style.setProperty(`--seg-1`, this.segments[1])
    }
  }
</script>

<style scoped>
  /* Import Exo 2 font */
  @import url('https://fonts.googleapis.com/css?family=Exo+2');

  /* Variables */
  #svg {
    /*--x-colour: #4A37BC;*/
    --x-colour: #E31133;
    --x-font: '\'Exo 2\'';

    --seg-0: #009DE7;
    --seg-1: #00A8F7;
  }

  /* SVG Styling */
  .st0 {
    fill: #FFFFFF;
    stroke: #000000;
    stroke-width: 1.5;
    stroke-miterlimit: 10;
  }

  .st1 {
    fill: none;
    stroke: #000000;
    stroke-width: 0.5;
    stroke-miterlimit: 10;
  }

  .st2 {
    font-family: var(--x-font), sans-serif;
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
