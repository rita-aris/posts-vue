<template>
  <div class="pagination">
    <div class="page" :class="{'active': page === pageNumber}" v-for="pageNumber in totalPages" :key="pageNumber" @click="$emit('change', pageNumber)"> {{ pageNumber }}</div>
  </div>
</template>

<script>
export default {
  name: "MyPagination",
  props: {
    totalPages: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    }
  },
}
</script>

<style scoped>
.pagination {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 30px;
}
.page {
  font-size: 12px;
  text-align: center;
  width: 25px;
  border-radius: 50%;
  cursor: pointer;
  padding: 5px;
  transition: 0.3s ease-in-out;
  &.active {
    background-color: #8cacee;
    color: #fff;
  }
  &:not(.active):hover {
    background-color: #8cacee;
    color: #fff;
    opacity: 0.3;
  }
}
</style>