<template>
  <div class="backdrop">
      <div class="modal">
        <div class="title">{{ title }}</div>
        <div class="subtitle">{{ subtitle }}</div>
        <slot></slot>
        <button @click="handleClick">Close</button>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        title: String,
        subtitle: String,
    },
    methods: {
        handleClick() {
            this.$emit('closeModal');
        },
    },
};
</script>

<style>
  .backdrop {
    top: 0;
    position: fixed;
    width: 100%;
    height: 100%;
    background-color: gray;
  }

  .modal {
    width: 100%;
    max-width: 655px;
    padding: 30px 112px 30px 112px;
    margin: 100px auto;
    background: #FFFFFF 0% 0% no-repeat padding-box;
    box-shadow: 0px 0px 40px #00000080;
    border-radius: 5px;
  }

  .modal .title {
    font-size: 20px;
    font-weight: bold;
    line-height: 13px;
    letter-spacing: 0px;
    color: #323232;
    margin: 22px 0px 8px 0px;
  }

  .modal .subtitle {
    font-size: 13px;
    line-height: 20px;
    margin-bottom: 31px;
  }

  .inactive {
    display: none;
  }

</style>