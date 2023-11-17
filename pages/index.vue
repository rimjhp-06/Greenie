<template>
  <div>
    <div class="tabs">
      <button class="tablinks" @click="openTab('userDetails')">User Details</button>
      <button class="tablinks">Account Creation</button>
    </div>

    <div v-if="activeTab === 'userDetails'" class="tabcontent">
      <h2>User Details</h2>
      <input v-model="searchQuery" type="text" placeholder="Search users..." />
      <table class="user-table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Username</th>
            <th>Email</th>
            <th>Phone</th>
            <th>Creation Date</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in filteredUsers" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.username }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.creationDate }}</td>
            <td>
              <button @click="generateReport(user.id)">Generate Report</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div v-if="activeTab === 'accountCreation'" class="tabcontent">
      <h2>Account Creation</h2>
      <!-- Add your account creation form here -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 'userDetails',
      users: [],
      searchQuery: '',
    };
  },
  async mounted() {
    // Fetch user data on component mount
    const { data } = await this.$axios.get('/api/users');
    this.users = data;
  },
  computed: {
    filteredUsers() {
      // Filter users based on the search query
      return this.users.filter(user =>
        user.username.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    openTab(tabName) {
      this.activeTab = tabName;
    },
    generateReport(userId) {
      // Implement logic to open a popup/modal and generate a report for the selected user
      alert(`Generate report for user with ID ${userId}`);
    },
  },
};
</script>

<style scoped>
/* Add your styling here using Tailwind CSS classes */
</style>
