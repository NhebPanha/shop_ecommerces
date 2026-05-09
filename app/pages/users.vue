<template>
  <div class="users-page">
    <div class="page-header">
      <div class="title">
        <h2>Customers</h2>
        <p>Manage and view your customer database</p>
      </div>
      <button class="add-btn">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><line x1="19" x2="19" y1="8" y2="14"/><line x1="22" x2="16" y1="11" y2="11"/></svg>
        Add Customer
      </button>
    </div>

    <div class="filters glass">
      <div class="search-box">
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
        <input type="text" placeholder="Search by name, email..." />
      </div>
      <div class="filter-actions">
        <select class="filter-select">
          <option>All Status</option>
          <option>Active</option>
          <option>Inactive</option>
        </select>
        <button class="icon-btn">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18"/><path d="M7 12h10"/><path d="M10 18h4"/></svg>
        </button>
      </div>
    </div>

    <div class="users-list glass">
      <table>
        <thead>
          <tr>
            <th>Customer</th>
            <th>Email</th>
            <th>Orders</th>
            <th>Total Spent</th>
            <th>Status</th>
            <th>Joined</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.email">
            <td>
              <div class="user-cell">
                <img :src="user.avatar" :alt="user.name" />
                <span class="name">{{ user.name }}</span>
              </div>
            </td>
            <td class="email">{{ user.email }}</td>
            <td>{{ user.orders }}</td>
            <td class="spent">${{ user.spent }}</td>
            <td>
              <span class="status-pill" :class="user.status.toLowerCase()">
                {{ user.status }}
              </span>
            </td>
            <td class="date">{{ user.joined }}</td>
            <td>
              <button class="more-btn">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="1"/><circle cx="19" cy="12" r="1"/><circle cx="5" cy="12" r="1"/></svg>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
const users = ref([])

onMounted(() => {
  const savedUsers = localStorage.getItem('users')
  if (savedUsers) {
    users.value = JSON.parse(savedUsers)
  } else {
    users.value = [
      { name: 'Olivia Johanson', email: 'olivia@example.com', avatar: 'https://i.pravatar.cc/150?u=olivia', orders: 12, spent: '1,240.50', status: 'Active', joined: 'Jan 12, 2024' },
      { name: 'Marcus Wright', email: 'marcus.w@example.com', avatar: 'https://i.pravatar.cc/150?u=marcus', orders: 5, spent: '450.00', status: 'Active', joined: 'Feb 05, 2024' },
      { name: 'Isabella Rossi', email: 'i.rossi@example.com', avatar: 'https://i.pravatar.cc/150?u=isabella', orders: 2, spent: '120.00', status: 'Inactive', joined: 'Mar 15, 2024' },
      { name: 'Nathan Drake', email: 'drake@uncharted.com', avatar: 'https://i.pravatar.cc/150?u=nathan', orders: 24, spent: '3,890.00', status: 'Active', joined: 'Jan 20, 2023' },
      { name: 'Sophia Miller', email: 'sophia.m@example.com', avatar: 'https://i.pravatar.cc/150?u=sophia', orders: 8, spent: '890.00', status: 'Active', joined: 'Apr 02, 2024' },
    ]
    saveToStorage()
  }
})

function saveToStorage() {
  localStorage.setItem('users', JSON.stringify(users.value))
}
</script>

<style scoped>
.users-page {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.title h2 { font-size: 1.75rem; font-weight: 700; margin-bottom: 4px; }
.title p { color: var(--text-muted); font-size: 0.9rem; }

.add-btn {
  background: var(--accent);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 12px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 4px 15px var(--accent-glow);
}

.add-btn:hover { transform: translateY(-2px); filter: brightness(1.1); }

.filters {
  display: flex;
  justify-content: space-between;
  padding: 16px 24px;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  padding: 8px 16px;
  border-radius: 10px;
  width: 350px;
}

.search-box input {
  background: transparent;
  border: none;
  color: var(--text-main);
  outline: none;
  width: 100%;
}

.filter-actions {
  display: flex;
  gap: 12px;
}

.filter-select {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  color: var(--text-main);
  padding: 8px 16px;
  border-radius: 10px;
  outline: none;
}

.icon-btn {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  color: var(--text-muted);
  width: 40px;
  height: 40px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.users-list {
  padding: 0;
  overflow: hidden;
}

table { width: 100%; border-collapse: collapse; }
th { text-align: left; color: var(--text-muted); font-weight: 500; font-size: 0.85rem; padding: 16px 24px; border-bottom: 1px solid var(--border); }
td { padding: 16px 24px; border-bottom: 1px solid var(--border); font-size: 0.9rem; }
tr:last-child td { border-bottom: none; }

.user-cell { display: flex; align-items: center; gap: 12px; }
.user-cell img { width: 36px; height: 36px; border-radius: 50%; border: 2px solid var(--border); }
.name { font-weight: 600; }
.email { color: var(--text-muted); }
.spent { font-weight: 600; color: var(--accent); }

.status-pill {
  padding: 4px 10px;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
}

.status-pill.active { background: rgba(34, 197, 94, 0.1); color: #22c55e; }
.status-pill.inactive { background: rgba(255, 255, 255, 0.05); color: var(--text-muted); }

.more-btn { background: transparent; border: none; color: var(--text-muted); cursor: pointer; }
</style>
