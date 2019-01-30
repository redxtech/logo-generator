<template>
  <div id="svg">
    <!--suppress CssUnknownProperty -->
    <svg
      version="1.1"
      xmlns="http://www.w3.org/2000/svg"
      x="0px"
      y="0px"
      viewBox="0 0 620 620"
      style="enable-background:new 0 0 620 620;"
    >
      <!-- Outer and inner bounds of hexagon -->
      <polygon
        class="hexagon"
        points="51.6,156.4 51.6,463.7 310.1,617.4 568.5,463.7 568.5,156.4 310.1,2.8"
      />
      <polygon
        class="hexagon"
        points="144.7,211.8 144.7,408.5 310.1,506.8 475.4,408.5 475.4,211.8 310.1,113.5"
      />
      <!-- X in middle of hexagon -->
      <path
        class="x"
        d=" M 375.363 432.18 L 314.475 317.484 L 305.271 317.484 L 244.737 432.18 L 210.753 432.18 L 279.429 305.802 L 215.355 187.92 L 248.985 187.92 L 304.917 293.412 L 315.183 293.412 L 371.115 187.92 L 404.745 187.92 L 340.317 305.802 L 409.347 432.18 L 375.363 432.18 Z "
      />
      <!--Segments to fill in hexagon-->
      <polygon
        class="segment0"
        points="310.1,2.8 568.5,156.4 475.4,211.8 310.1,113.5"
      />
      <polygon
        class="segment1"
        points="568.5,156.4 568.5,463.7 475.4,408.5 475.4,211.8"
      />
      <polygon
        class="segment0"
        points="568.5,463.7 310.1,617.4 310.1,506.8 475.4,408.5"
      />
      <polygon
        class="segment1"
        points="310.1,617.4 51.6,463.7 144.7,408.5 310.1,506.8"
      />
      <polygon
        class="segment0"
        points="51.6,463.7 51.6,156.4 144.7,211.8 144.7,408.5"
      />
      <polygon
        class="segment1"
        points="51.6,156.4 310.1,2.8 310.1,113.5 144.7,211.8"
      />
      <!-- Hexagon lines -->
      <line
        class="line"
        x1="310.1"
        y1="2.8"
        x2="310.1"
        y2="113.5"
      />
      <line
        class="line"
        x1="568.5"
        y1="156.4"
        x2="475.4"
        y2="211.8"
      />
      <line
        class="line"
        x1="568.5"
        y1="463.7"
        x2="475.4"
        y2="408.5"
      />
      <line
        class="line"
        x1="310.1"
        y1="617.4"
        x2="310.1"
        y2="506.8"
      />
      <line
        class="line"
        x1="51.6"
        y1="463.7"
        x2="144.7"
        y2="408.5"
      />
      <line
        class="line"
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
      xBorder: {
        type: String,
        required: false,
        default: '#E31133'
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
      },
      strokeThickness: {
        type: Number,
        required: false,
        default: 0.0
      }
    },
    data () {
      return {
        svg: undefined
      }
    },
    watch: {
      xColour (val) {
        this.svg.style.setProperty('--x-colour', val)
      },
      segments () {
        this.svg.style.setProperty(`--segment-0`, this.segments[0])
        this.svg.style.setProperty(`--segment-1`, this.segments[1])
      },
      xBorder (val) {
        this.svg.style.setProperty('--x-border', val)
      },
      thickness () {
        this.svg.style.setProperty(`--border-thickness`, this.thickness)
      },
      lineThickness () {
        this.svg.style.setProperty(`--line-thickness`, this.lineThickness)
      },
      strokeThickness () {
        this.svg.style.setProperty(`--stroke-thickness`, this.strokeThickness)
      }
    },
    mounted () {
      const svg = window.document.querySelector('#svg')
      this.svg = svg
      svg.style.setProperty('--x-color', this.xColour)
      svg.style.setProperty('--x-border', this.xBorder)
      svg.style.setProperty(`--segment-0`, this.segments[0])
      svg.style.setProperty(`--segment-1`, this.segments[1])
      svg.style.setProperty(`--border-thickness`, this.thickness)
      svg.style.setProperty(`--line-thickness`, this.lineThickness)
      svg.style.setProperty(`--stroke-thickness`, this.strokeThickness)
    }
  }
</script>

<style>
  /* Variables */
  #svg {
    --x-colour: #E31133;
    --segment-0: #009DE7;
    --segment-1: #00A8F7;
    --x-border: #E31133;
    --border-thickness: 1.5;
    --line-thickness: 0.0;
    --stroke-thickness: 0.0;

    margin: 1rem auto;
    max-width: 400px;
    max-height: 400px;
  }

  /* SVG Styling */
  .hexagon {
    fill: #FFFFFF;
    stroke: #000000;
    stroke-width: var(--border-thickness);
    stroke-miterlimit: 10;
  }

  .line {
    fill: none;
    stroke: #000000;
    stroke-width: var(--line-thickness);
    stroke-miterlimit: 10;
  }

  .x {
    stroke: var(--x-border);
    stroke-width: var(--stroke-thickness);
    fill: var(--x-colour);
  }

  .segment0 {
    fill: var(--segment-0);
  }

  .segment1 {
    fill: var(--segment-1);
  }
</style>
