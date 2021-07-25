<template>
  <div class="backdrop">
      <div class="modal">
        <div class="padded-content">
            <div @click="handleClick" class="close"/>
            <div class="title">{{ title }}</div>
            <div class="subtitle">{{ subtitle }}</div>
            <slot></slot>
          </div>
        <slot name="footer"></slot>
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
    position: relative;
    width: 100%;
    max-width: 655px;
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
    margin: 12px 0px 8px 0px;
  }

  .modal .subtitle {
    font-size: 13px;
    line-height: 20px;
    margin-bottom: 31px;
  }

  .padded-content {
      padding: 52px 112px 0px 112px;
  }

  .inactive {
    display: none;
  }

  .close {
    position: absolute;
    top: 30px;
    right: 30px;
    width: 32px;
    height: 32px;
    opacity: 0.3;
    cursor: pointer;
}
.close:hover {
  opacity: 1;
}
.close:before, .close:after {
  position: absolute;
  left: 15px;
  content: ' ';
  height: 15px;
  width: 2px;
  background-color: #333;
}
.close:before {
  transform: rotate(45deg);
}
.close:after {
  transform: rotate(-45deg);
}

</style>