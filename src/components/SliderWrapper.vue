<template>
  <div>
    <div class="slider-title slider-top-title">
      <div class="slider-top-left-title">{{sliderLeftTopTitle}}</div>
      <div class="slider-top-right-title">{{this.mutableSliderRightTopTitle}}<span class="symbol" v-bind:class="renderSymbolFontSize">{{ renderWhitespace }}{{ symbol }}</span></div>
    </div>
    <Slider @emitValue="sliderValueCallback" :minValue="minValue" :maxValue="maxValue"/>
    <div class="slider-title slider-bottom-title">
      <div>{{minValue}}<span>{{ renderWhitespace }}{{ symbol }}</span></div>
      <div>{{renderFormattedValue}}<span>{{ renderWhitespace }}{{ symbol }}</span></div>
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
    name: String,
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
            this.$emit('updateSlider', {sliderName: this.name, value})
        },
    },
    computed: {
      renderFormattedValue() {
         return this.formattedValue(this.maxValue);
      },
      renderWhitespace() {
        return this.name === 'duration' ? ' ' : null;
      },
      renderSymbolFontSize() {
        return this.name === 'duration' ? 'symbol-small' : 'symbol-big';
      }
    }
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
  margin-bottom: 16px;
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

.symbol-big {
  font-size: 20px;
}

.symbol-small {
 font-size: 15px;
}
</style>
