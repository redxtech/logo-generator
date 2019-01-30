<template>
  <div id="app">
    <SVGGenerator
      :x-colour="colour"
      :segments="segments"
      :x-border="border"
      :thickness="thickness"
      :line-thickness="lineThickness"
      :stroke-thickness="strokeThickness"
    />
    <div class="container">
      <div class="columns">
        <div class="column is-offset-1">
          <form class="form">
            <div class="field">
              <div class="in in0">
                <label class="label">X Colour</label>
                <sketch
                  v-model="xColour"
                  :presetColors="xColourPresets"
                />
              </div>
              <div class="in in1">
                <label class="label">X Border Colour</label>
                <sketch
                  v-model="xBorder"
                  :presetColors="xColourPresets"
                />
              </div>
              <div class="in in1">
                <label class="label">Segment Colour 1</label>
                <sketch
                  v-model="segment0"
                  :presetColors="segmentPresets"
                />
              </div>
              <div class="in in2">
                <label class="label">Segment Colour 2</label>
                <sketch
                  v-model="segment1"
                  :presetColors="segmentPresets"
                />
              </div>
            </div>
            <div class="field">
              <label class="label">Border Thickness</label>
              <div class="slider">
                <vue-slider
                  v-model="thickness"
                  :min="0"
                  :max="10"
                  :interval="0.1"
                ></vue-slider>
              </div>
            </div>
            <div class="field">
              <label class="label">Line Thickness</label>
              <div class="slider">
                <vue-slider
                  v-model="lineThickness"
                  :min="0"
                  :max="10"
                  :interval="0.1"
                ></vue-slider>
              </div>
            </div>
            <div class="field">
              <label class="label">X Border Thickness</label>
              <div class="slider">
                <vue-slider
                  v-model="strokeThickness"
                  :min="0"
                  :max="3"
                  :interval="0.1"
                ></vue-slider>
              </div>
            </div>
            <div class="field">
              <label class="label">Size (px) NOT WORKING</label>
              <div class="control">
                <input v-model="size" class="input" type="number" placeholder="1024">
              </div>
            </div>
            <div class="field has-addons">
              <div class="control">
                <input v-model="filename" class="input" type="text" placeholder="Logo.png">
              </div>
              <div class="control">
                <a
                  class="button is-info"
                  @click="save"
                >
                  Export PNG
                </a>
              </div>
            </div>
            <div class="field has-addons">
              <div class="control">
                <input v-model="svgname" class="input" type="text" placeholder="Logo.svg">
              </div>
              <div class="control">
                <a
                  class="button is-info"
                  @click="saveSVG"
                >
                  Export SVG
                </a>
              </div>
            </div>
            <div class="field">
              <div class="control">
                <button class="button is-info in0" @click="reset">Reset</button>
              </div>
            </div>
          </form>
        </div>
        <div class="column is-1" />
      </div>
    </div>
  </div>
</template>

<script>
  import SVGGenerator from './components/SVGComponent.vue'
  import { Sketch } from 'vue-color'
  import VueSlider from 'vue-slider-component'
  import { saveSvgAsPng, saveSvg } from 'save-svg-as-png'

  export default {
    name: 'app',
    components: {
      SVGGenerator,
      Sketch,
      VueSlider
    },
    data () {
      return {
        xColour: {
          hex: '#E31133'
        },
        segment0: {
          hex: '#009DE7'
        },
        segment1: {
          hex: '#00A8F7'
        },
        xBorder: {
          hex: '#E31133'
        },
        xColourPresets: ['#E31133', '#4A37BC'],
        segmentPresets: ['#009DE7', '#00A8F7'],
        thickness: 1.5,
        lineThickness: 0.0,
        strokeThickness: 0.0,
        filename: 'Logo.png',
        svgname: 'Logo.svg',
        size: 1024
        // size: 2048
      }
    },
    computed: {
      colour () {
        return this.xColour.hex
      },
      border () {
        return this.xBorder.hex
      },
      segments () {
        return [
          this.segment0.hex,
          this.segment1.hex
        ]
      },
      scale () {
        return (this.size / 1085) + 0.00055
      }
    },
    methods: {
      modifyStyle (styles) {
        return styles
          .replace('var(--x-colour)', this.xColour.hex)
          .replace('var(--segment-0)', this.segment0.hex)
          .replace('var(--segment-1)', this.segment1.hex)
          .replace('var(--x-border-colour)', this.xBorder)
          .replace('var(--border-thickness)', this.thickness)
          .replace('var(--line-thickness)', this.lineThickness)
          .replace('var(--stroke-thickness)', this.strokeThickness)
      },
      reset (e) {
        e.preventDefault()
        this.xColour = {
          hex: '#E31133'
        }
        this.segment0 = {
          hex: '#009DE7'
        }
        this.segment1 = {
          hex: '#00A8F7'
        }
        this.xBorder = {
          hex: '#E31133'
        }
        this.thickness = 1.5
        this.lineThickness = 0.0
        this.strokeThickness = 0.0
      },
      save (e) {
        e.preventDefault()
        saveSvgAsPng(document.querySelector('#svg svg'), this.filename, {
          encoderOptions: 1,
          // scale: this.scale,
          modifyStyle: this.modifyStyle
        })
      },
      saveSVG (e) {
        e.preventDefault()
        saveSvg(document.querySelector('#svg svg'), this.svgname, {
          modifyStyle: this.modifyStyle
        })
      }
    }
  }
</script>

<style>
  @import url('https://cdnjs.cloudflare.com/ajax/libs/bulma/0.7.2/css/bulma.min.css');

  body {
    margin: 0;
  }

  .in {
    display: inline-block;
  }

  .in0 {
    padding-right: 1rem;
  }

  .in1 {
    padding-left: 1rem;
    padding-right: 1rem;
  }

  .in2 {
    padding-left: 1rem;
  }

  .slider {
    padding-top: 2rem;
  }
</style>
