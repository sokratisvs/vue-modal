<template>
<div class="container">
<div class="form-row">
    <div class="row-cell description">
        {{ description }}
    </div>
    <form class="row-cell input-block">
    <input
      :name="inputName"
      v-model="fieldValue"
      :type="type"
      :placeholder="placeholderText"
    />
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
  },
    data() {
      return {
            result: '',
            fieldValue: '',
            placeholderText: this.placeholder,
      };
  },
   methods: {
        checkForm(e) {
          e.preventDefault();
          const regex = new RegExp(/^\+?[0-9]{10}$/);
          const isValueValid = regex.test(this.fieldValue);
            if (isValueValid) {
              // eslint-disable-next-line no-return-assign
                return this.result = 'Επιτυχής καταχώριση!';
            }

            if (!isValueValid) {
              // eslint-disable-next-line no-return-assign
                return this.result = 'Tο στοιχείο που καταχωρήσατε ειναι λάθος';
            }
            return true;
        },
    },
        watch:{
        fieldValue: function (newtargetValue, oldTargetValue){
          if(newtargetValue !== oldTargetValue) {
            this.result = '';
          }
        },
    }
}
</script>

<style>
.container {
    width: 100%;
    height: 125px;
    background-color: #223657;
    display: flex;
    align-items: center;
    border-radius: 0px 0px 5px 5px;
}

.form-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 45px;
    padding: 0px 30px 0px 30px;
}

.row-cell {
  position: relative;
    display: flex;
    flex-wrap: wrap;
    color: #FFFFFF;
    height: 100%;
}

.description {
  width: 40%;
  text-align: left;
}

.input-block {
   width: 60%;
   display: flex;
   justify-content: flex-end;
}

input {
  width: 216px;
  display: block;
  box-sizing: border-box;
  border: 1px solid #E4E4E4;
  border-radius: 5px 0px 0px 5px;
}

input::placeholder {
  text-align: left;
  letter-spacing: 0px;
  color: #9E9E9E;
  opacity: 1;
}

.button {
  width: 100px;
  background-color: #55AC36;
  background: #55AC36 0% 0% no-repeat padding-box;
  border-radius: 0px 5px 5px 0px;
  text-align: center;
  letter-spacing: 0px;
  color: #FFF;
  font-size: 14px;
  font-weight: 500;
  text-transform: uppercase;
  border: none;
  cursor: pointer;
}

.result {
  position: absolute;
  bottom: -35px;
  font-size: 14px;
  color: white;
}
</style>