<template>
  <div>
    <div class="slider-title slider-top-title">
      <div class="slider-top-left-title">{{sliderLeftTopTitle}}</div>
      <div class="slider-top-right-title">{{this.mutableSliderRightTopTitle}}<span class="symbol">{{ symbol }}</span></div>
    </div>
    <Slider @emitValue="sliderValueCallback" :minValue="minValue" :maxValue="maxValue"/>
    <div class="slider-title slider-bottom-title">
      <div>{{minValue}}{{ symbol }}</div>
      <div>{{this.formattedValue(maxValue)}}<span>{{ symbol }}</span></div>
    </div>
  </div>
</template>

<script>
import Slider from './Slider.vue';

export default {
  name: 'SliderWrapper',
  components: {
      Slider,
  },
  props: {
    sliderLeftTopTitle: String,
    sliderRightTopTitle: Number,
    symbol: String,
    minValue: Number,
    maxValue: Number,
  },
      data() {
        return {
             mutableSliderRightTopTitle: this.sliderRightTopTitle
        };
    },
   methods: {
        formattedValue(value) {
          return value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
        },
        sliderValueCallback(value) {
            this.mutableSliderRightTopTitle = this.formattedValue(value);
        },
    },
}
</script>

<style>
.slider-title {
  display: flex;
  justify-content: space-between;
  align-content: center;
}

.slider-top-title {
  font-weight: bold;
  margin-bottom: 29px;
}

.slider-bottom-title {
  color: #B7C8D0;
  margin-bottom: 20px;
  font-size: 14px;
  line-height: 16px;
}

.slider-top-left-title {
  text-align: left;
  font-size: 15px;
  line-height: 20px;
}

.slider-top-right-title {
  text-align: right;
  font-size: 24px;
  line-height: 16px;
}

.symbol {
  font-size: 20px;
}
</style>
