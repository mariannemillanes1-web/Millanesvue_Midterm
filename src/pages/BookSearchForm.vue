<template>
  <form @submit.prevent="submitForm" class="my-4">
    <div class="mb-3">
      <label class="form-label">Search Book Title</label>
      <input type="text" class="form-control" v-model="searchQuery" />
      <div class="text-danger" v-if="error">{{ error }}</div>
    </div>
    <button class="btn btn-primary" type="submit">Search</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      error: ''
    }
  },
  methods: {
    submitForm() {
      if (this.searchQuery.trim() === '') {
        this.error = 'Please enter a book title.'
        return
      }
      this.error = ''
      this.$emit('search-books', this.searchQuery)
    }
  }
}
</script>
