<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: [],
      currentPage: 1,
      totalPages: null,
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      axios.get('/api/users', { params: { page: this.currentPage } })
        .then(response => {
          this.users = response.data.data;
          this.currentPage = response.data.current_page;
          this.totalPages = response.data.last_page;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>
<template>
    <div>

    </div>
</template>

<style scoped>

</style>