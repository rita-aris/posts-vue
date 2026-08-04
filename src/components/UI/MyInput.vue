<template>
  <input class="input" type="text" :value="modelValue" @input="updateInput">
</template>

<script>
export default {
  name: 'MyInput',
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>
.input {
  width: 100%;
  border: none;
  box-shadow: 0 0 10px 0 #8cacee;
  padding: 10px;
  margin-top: 15px;
  &:focus {
    outline: #0048D9 solid 2px;
  }
  &::placeholder {
    color: #B8BCCA;
  }
}
</style>