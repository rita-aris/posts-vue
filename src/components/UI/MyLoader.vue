<template>
  <span class="loader"></span>
</template>

<script>
export default {}
</script>

<style scoped>
.loader {
  position: relative;
  display: block;
  color: #8cacee;
  width: 48px;
  height: 48px;
  margin: 20px auto;
  animation: rotation 1s linear infinite;
  &:after, &:before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 24px;
    height: 24px;
    background-color: #8cacee;
    border-radius: 50%;
    transform: scale(0.5) translate(0, 0);
    animation: bubble 1s infinite ease-in-out;
  }
  &:before {
    background-color: #0048D9;
    transform: scale(0.5) translate(-48px, -48px);
  }
}
@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes bubble {
  50% {
    transform: scale(1) translate(-50%, -50%);
  }
}
</style>