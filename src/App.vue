<template>
<div>
  <div v-if="showModal">
    <Modal :title="title" :subtitle="subtitle" @closeModal="toggleModal">
      <div v-for="item in modalSliderItems" :key="item.symbol">
        <template>
          <SliderWrapper 
            :name="item.name"
            :symbol="item.symbol" 
            :sliderLeftTopTitle="item.sliderLeftTopTitle"
            :sliderRightTopTitle="item.sliderRightTopTitle"
            :minValue="item.minValue" 
            :maxValue="item.maxValue"
            @updateSlider="updateSliderCallback"
          />
        </template>
      </div>
      <p class="result-title">Μηνιαία Δόση: <span class="result-value">{{ calculateMonthlyValue }}</span><span class="result-symbol">€</span></p>
      <template v-slot:footer>
        <div>
      <FormInput 
        :description="formInputDescription" 
        :inputName="formInputName" 
        :placeholder="formInputPlaceholder" 
        :cta="formInputCTA"
        :type="formInputType"
        @inputValue="updateInputValue"
      />
      </div>
      </template>
    </Modal>
  </div>
  <button @click="toggleModal">Show Modal</button>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';
import SliderWrapper from './components/SliderWrapper.vue';
import FormInput from './components/FormInput.vue';

export default {
    name: 'App',
    components: {
        Modal,
        SliderWrapper,
        FormInput,
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
                name: 'downPayment',
              },
              { 
                sliderLeftTopTitle: 'Διάρκεια',
                sliderRightTopTitle: 3,
                minValue: 3,
                maxValue: 72,
                symbol: 'μήνες', 
                name: 'duration',
              }
            ],
            sliderData: {
              downPayment: 0,
              duration: 3,
            },
            formInputDescription: 'Συμπλήρωσε εδώ το τηλέφωνό σου. Θα σε καλέσουμε άμεσα.',
            formInputName: 'telephone',
            formInputPlaceholder: 'Αριθμός τηλεφώνου…',
            formInputCTA: 'Καλεστε',
            formInputType: 'tel',
            icon: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='25' height='25' viewBox='0 0 25 25' fill-rule='evenodd'%3E%3Cpath d='M16.036 18.455l2.404-2.405 5.586 5.587-2.404 2.404zM8.5 2C12.1 2 15 4.9 15 8.5S12.1 15 8.5 15 2 12.1 2 8.5 4.9 2 8.5 2zm0-2C3.8 0 0 3.8 0 8.5S3.8 17 8.5 17 17 13.2 17 8.5 13.2 0 8.5 0zM15 16a1 1 0 1 1 2 0 1 1 0 1 1-2 0'%3E%3C/path%3E%3C/svg%3E"
        };
    },
    methods: {
        toggleModal() {
            this.showModal = !this.showModal;
        },
        updateSliderCallback(data) {
          this.$set(this.sliderData, `${[data.sliderName]}`, data.value)
          return this.sliderData;
        },
        formattedValue(value) {
          const formattedThousands = value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.');
          return formattedThousands.replace(/.([^.]*)$/, ",$1");
        },
        updateInputValue(value) {
          this.formInputValue = value;
        }
    },
    computed: {
      calculateMonthlyValue: function () {
          const finalPrice = 20000;
          const subtraction = parseInt(finalPrice, 10) - parseInt(this.sliderData.downPayment, 10);
          const result = subtraction / parseInt(this.sliderData.duration, 10);
          return this.formattedValue(result.toFixed(2));
        }
    }
};
</script>

<style>
.result-title {
  font-size: 15px;
  line-height: 20px;
  font-weight: bold;
  line-height: 20px;
  margin-bottom: 29px;
}

.result-value {
  font-size: 24px;
  line-height: 13px;
}

.result-symbol {
  font-size: 20px;
  line-height: 16px;
}

@media (max-width: 600px) {
  .result-value {
      display: inline-block;
      margin-top: 12px;
    }
}
</style>