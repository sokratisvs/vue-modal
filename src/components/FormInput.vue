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
    icon: String
  },
    data() {
      return {
            result: '',
            fieldValue: '',
            placeholderText: this.placeholder,
            inputIcon: this.icon,
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
    },
}
</script>

<style>
.container {
    height: 125px;
    background-color: #223657;
    display: flex;
    align-items: center;
    border-radius: 0px 0px 5px 5px;
    padding: 0px 30px 0px 30px;
}

.form-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}

.row-cell {
    position: relative;
    height: 45px;
    display: flex;
    flex-wrap: wrap;
    color: #FFF;
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
  height: 100%;
  display: block;
  box-sizing: border-box;
  border: 1px solid #E4E4E4;
  border-radius: 5px 0px 0px 5px;
}

input::placeholder {
  text-align: left;
  padding-left: 46px;
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

@media (max-width: 600px) {
  .container {
    justify-content: center;
    height: 150px;
  }
  .form-row {
      flex-direction: column;
    }
  .row-cell {
      width: 100%;

      flex-wrap: nowrap;
      text-align: center;
  }
  .input-block {
    justify-content: center;
  }
}

@media (max-width: 375px) {
    .container {
      padding-bottom: 20px;
    }

  input {
    width: 185px;
  }
  .result {
    bottom: -40px;
  }

}
</style>