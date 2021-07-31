<template>
  <div>
    <vue-slider 
        class="slider" 
        :min="minValue" 
        :max="maxValue" 
        :interval="step" 
        v-model="sliderValue" 
        @change="emitValue" 
        :dotSize="dotSize"
        :railStyle="railStyle"
        :tooltipStyle="toolTipStyle"
        :processStyle="processStyle"
        :dotStyle="dotStyle"
    >
    </vue-slider>
  </div>
</template>

<script>
import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/default.css'

export default {
    name: 'Slider',
    props: {
        minValue: Number,
        maxValue: Number,
    },
    data() {
        return {
            sliderValue: this.minValue,
            step: 1,
            dotSize: 26,
            toolTipStyle: {
                'background-color': '#01AED8',
                'border-color': '#01AED8',
            },
            railStyle: {
                height: '8px',
                'background-color': '#D8D8D8',
                'border-radius': '9px'
            },
            processStyle: {
                'background-color': '#01AED8',
            },
            dotStyle: {
                'box-shadow': '0px 0px 10px #00000033',
            }
        };
    },
    components: {
        VueSlider
    },
    methods: {
        emitValue() {
            this.$emit('emitValue', parseInt(this.sliderValue));
        },
    },
};
</script>

<style>
  .slider {
    width: 100%;
  }

  .vue-range-slider.slider-component {
    padding: 13px 0px 13px 0px !important;
  }
</style> 