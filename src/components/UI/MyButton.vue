<template>
  <button class="btn" :class="customClass">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'MyButton',
  props: {
    customClass: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
.btn {
  border: none;
  color: #fff;
  background-color: #0048D9;
  border-radius: 6px;
  cursor: pointer;
  padding: 10px;
  transition: 0.3s ease-in-out;
  &:hover {
    background-color: #002266;
  }
  &:disabled {
    background-color: #8cacee;
    cursor: auto;
  }
}
.btn_end {
  align-self: flex-end;
  margin-top: 15px;
}
@media screen and (max-width: 480px) {
  .btn_end {
    align-self: flex-start;
  }
}
</style>