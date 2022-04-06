<template>
  <div class="container search">
    <input
      v-model.lazy="searchInput"
      type="text"
      placeholder="Search for an user"
      @keyup.enter="$emit('searchValue', searchInput)"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchModal',
  props: {
    searchVal: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      searchInput: '',
    }
  },
  watch: {
    searchVal(newVal, oldVal) {
      this.searchInput = newVal
    },
  },
}
</script>

<style scoped>
.search {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 32px 16px;
}

input {
  max-width: 1000px;
  width: 100%;
  padding: 12px 6px;
  font-size: 14px;
  border: 1px solid white;
}

input:focus {
  outline: none;
}
</style>