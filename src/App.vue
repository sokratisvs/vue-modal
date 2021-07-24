<template>
<div>
  <div v-if="showModal">
    <Modal :title="title" :subtitle="subtitle" @closeModal="toggleModal">
      <div v-for="item in modalSliderItems" :key="item.symbol">
        <template>
          <SliderWrapper 
            :symbol="item.symbol" 
            :sliderLeftTopTitle="item.sliderLeftTopTitle"
            :sliderRightTopTitle="item.sliderRightTopTitle"
            :minValue="item.minValue" 
            :maxValue="item.maxValue" 
          />
        </template>
      </div>
    </Modal>
  </div>
  <button @click="toggleModal">Show Modal</button>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';
import SliderWrapper from './components/SliderWrapper.vue';

export default {
    name: 'App',
    components: {
        Modal,
        SliderWrapper,
    },
    data() {
        return {
            title: 'Υπολογισμός δόσης',
            subtitle: 'Επίλεξε την προκαταβολή και την διάρκεια που σε συμφέρει',
            showModal: false,
            modalSliderItems: [
              { 
                sliderLeftTopTitle: 'Προκαταβολή',
                sliderRightTopTitle: 0,
                minValue: 0,
                maxValue: 10700,
                symbol: '€', 
              },
              { 
                sliderLeftTopTitle: 'Διάρκεια',
                sliderRightTopTitle: 3,
                minValue: 3,
                maxValue: 72,
                symbol: 'μήνες', 
              }
            ],
            sliderLeftTopTitle: 'Προκαταβολή',
            sliderRightTopTitle: 0,
            minValue: 0,
            maxValue: 10700,
            symbol: '€',
        };
    },
    methods: {
        toggleModal() {
            this.showModal = !this.showModal;
        },
        formattedValue(value) {
          return value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
        },
        sliderValueCallback(value) {
            this.sliderRightTopTitle = this.formattedValue(value);
        },
    },
};
</script>

<style>
h1 {
  display: 'inline-block';
  border-bottom: 1px solid #2c3e50;
}
</style>