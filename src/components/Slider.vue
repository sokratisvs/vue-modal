<template>
  <div>
    <vue-range-slider 
        class="slider" 
        :min="minValue" 
        :max="maxValue" 
        :step="step" 
        v-model="sliderValue" 
        @slide-end="emitValue" 
        :dot-size="dotSize"
    >
      <template slot="knob">
        <div class="knobby">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 26 26" width="26" height="26">
            <path
              fill="#006F8A"
              fill-rule="evenodd"
              d="M9.864 20c5.243-5.195 7.864-9.24 7.864-12.136A7.863 7.863 0 009.864 0 7.863 7.863 0 002 7.864C2 10.759 4.621 14.804 9.864 20z"
            ></path>
          </svg>
        </div>
      </template>
    </vue-range-slider>
  </div>
</template>

<script>
import 'vue-range-component/dist/vue-range-slider.css'
import VueRangeSlider from 'vue-range-component'

export default {
  name: "Slider",
  props: {
    minValue: Number,
    maxValue: Number,
  },
  data() {
    return {
      sliderValue: this.minValue,
      step: 1,
      dotSize: 26,
    };
  },
  components: {
    VueRangeSlider
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

.slider .range-slider-rail {
  height: 11px;
  background-color: #D8D8D8;
  border-radius: 5px;
}

.slider .range-slider-fill {
  height: 3px;
  margin: 0 4px;
  background-color: #01AED8;
}

.slider .range-slider-knob {
  height: 26px;
  width: 26px;
  color: #fff;
  background-color: #01AED8;
  border: 0;
  box-shadow: 0 0 0 10px rgb(0 111 138 / 0.2);
}

.slider .knobby {
  position: relative;
}

.slider .knobby svg {
  width: 50px;
  height: 50px;
  position: absolute;
  top: -65px;
  left: -14px;
}

.slider .knobby svg text {
  font-size: 5px;
  font-weight: bold;
}

.vue-range-slider.slider-component .slider-tooltip-wrap .slider-tooltip {
    display: none;
}

.vue-range-slider.slider-component .slider .slider-dot {
      box-shadow: 0px 0px 10px #00000033;
}

.vue-range-slider.slider-component {
  padding: 13px 0px 13px 0px !important;
}
</style> 