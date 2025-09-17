<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Movie Finder</a>
        <div>
          <router-link class="btn btn-outline-light me-2" to="/">Home</router-link>
          <router-link class="btn btn-outline-light" to="/about">About</router-link>
        </div>
      </div>
    </nav>
    <div class="container mt-4">
      <router-view />
    </div>
  </div>
</template>

<script setup>
</script>
