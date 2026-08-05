<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div class="modal__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "MyModal",
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideModal() {
      this.$emit("update:show", false);
    }
  }
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 34, 102, 0.5);
  display: flex;
}
.modal__content {
  background-color: #ffffff;
  border-radius: 6px;
  width: 960px;
  padding: 20px;
  margin: auto;
}
@media screen and (max-width: 960px) {
  .modal__content {
    width: 90%;
  }
}
</style>