<template>
  <div class="container mt-4">
    <BookSearchForm @search-books="fetchBooks" />

    <div v-if="books.length > 0" class="row mt-4">
      <div v-for="book in books" :key="book.key" class="col-md-4 mb-3">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">{{ book.title }}</h5>
            <p class="card-text">Author: {{ book.author_name?.[0] || 'Unknown' }}</p>
            <p class="card-text">Year: {{ book.first_publish_year || 'N/A' }}</p>
          </div>
        </div>
      </div>
    </div>

    <div v-else-if="searched" class="text-danger mt-4">No results found.</div>
  </div>
</template>

<script>
import BookSearchForm from './BookSearchForm.vue'

export default {
  components: { BookSearchForm },
  data() {
    return {
      books: [],
      searched: false
    }
  },
  methods: {
    async fetchBooks(query) {
      this.books = []
      this.searched = false
      try {
        const res = await fetch(`https://openlibrary.org/search.json?title=${encodeURIComponent(query)}`)
        const data = await res.json()
        this.books = data.docs.slice(0, 9)
        this.searched = true
      } catch (err) {
        alert('Error fetching books')
      }
    }
  }
}
</script>
