<template>
<div class="form">
  <div class="form__row">
    <div class="form__cell description">
        {{ description }}
    </div>
      <form class="form__cell input--block">
      <div class="input__container">
        <span v-if="!hasFocus" class="icon" v-html="bgImage"/>
        <input
          :name="inputName"
          v-model="fieldValue"
          :type="type"
          :placeholder="placeholderText"
          @focus="hasFocus = true"
          @blur="setFocusAttribute"
        />
      </div>
      <button
        @click="checkForm"
        class="button"
      >
      {{ cta }}
      </button>
        <p v-if="result" class="result">
          {{ result }}
        </p>
    </form>
    </div>
  </div>
</template>

<script>
export default {
    name: 'FormInput',
    props: {
        description: String,
        inputName: String,
        placeholder: String,
        cta: String,
        type: String,
        icon: String
    },
    data() {
        return {
            result: '',
            fieldValue: '',
            placeholderText: this.placeholder,
            hasFocus: false,
        };
    },
    methods: {
        setFocusAttribute() {
            if(this.fieldValue.length === 0) {
                this.hasFocus = false;
            }
        },
        checkForm(e) {
            e.preventDefault();
            const regex = new RegExp(/^\+?[0-9]{10}$/);
            const isValueValid = regex.test(this.fieldValue);

            if (!isValueValid) {
                return this.result = 'Tο στοιχείο που καταχωρήσατε ειναι λάθος';
            }
            return this.result = 'Επιτυχής καταχώριση!';
        },
    },
    watch:{
        fieldValue: function (newtargetValue, oldTargetValue){
            if(newtargetValue !== oldTargetValue) {
                this.result = '';
            }
        },
    },
    computed: {
        bgImage () {
            return require(`!!raw-loader!@/assets/images//${this.icon}.svg`).default;
        },
    }
}
</script>

<style lang="scss">
@import './FormInput.scss';
</style>