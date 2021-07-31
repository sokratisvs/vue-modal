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

<style lang="scss">
@import './Modal.scss';
</style>