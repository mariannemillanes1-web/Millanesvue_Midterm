<template>
  <div>
    <h2>Student Registration</h2>

    <form @submit.prevent="handleSubmit" class="mb-4">
      <div class="mb-3">
        <label>Name</label>
        <input v-model="form.name" class="form-control" />
        <div class="text-danger" v-if="!form.name && submitted">Name is required.</div>
      </div>

      <div class="mb-3">
        <label>Email</label>
        <input v-model="form.email" class="form-control" />
        <div class="text-danger" v-if="!isValidEmail && submitted">Valid email is required.</div>
      </div>

      <div class="mb-3">
        <label>Search Students (by name)</label>
        <input v-model="form.search" class="form-control" />
      </div>

      <button class="btn btn-primary" type="submit">Submit</button>
    </form>

    <h4>Registered Students</h4>
    <ul class="list-group">
      <li class="list-group-item" v-for="user in filteredUsers" :key="user.id">
        {{ user.name }} - {{ user.email }}
      </li>
    </ul>
    <p v-if="filteredUsers.length === 0" class="text-muted mt-3">No students found.</p>
  </div>
</template>

<script>
import { ref, onMounted, computed } from 'vue';

export default {
  setup() {
    const form = ref({
      name: '',
      email: '',
      search: '',
    });

    const submitted = ref(false);
    const users = ref([]);

    const fetchUsers = async () => {
      try {
        const res = await fetch('https://jsonplaceholder.typicode.com/users');
        users.value = await res.json();
      } catch (error) {
        console.error(error);
      }
    };

    const handleSubmit = () => {
      submitted.value = true;
      if (form.value.name && isValidEmail.value) {
        alert('Student Registered!');
        form.value.name = '';
        form.value.email = '';
      }
    };

    const isValidEmail = computed(() =>
      /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email)
    );

    const filteredUsers = computed(() => {
      if (!form.value.search) return users.value;
      return users.value.filter((user) =>
        user.name.toLowerCase().includes(form.value.search.toLowerCase())
      );
    });

    onMounted(fetchUsers);

    return {
      form,
      users,
      filteredUsers,
      submitted,
      isValidEmail,
      handleSubmit,
    };
  },
};
</script>
