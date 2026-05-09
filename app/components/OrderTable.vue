<template>
  <div class="table-container glass">
    <div class="table-header">
      <h3>Recent Orders</h3>
      <button class="view-all">View All</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Order ID</th>
          <th>Customer</th>
          <th>Product</th>
          <th>Amount</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="order in orders" :key="order.id">
          <td class="id">#{{ order.id }}</td>
          <td>
            <div class="customer">
              <img :src="order.avatar" alt="Avatar" />
              {{ order.customer }}
            </div>
          </td>
          <td>{{ order.product }}</td>
          <td class="amount">${{ order.amount }}</td>
          <td>
            <span class="status" :class="order.status.toLowerCase()">
              {{ order.status }}
            </span>
          </td>
          <td>
            <button class="action-btn">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="1"/><circle cx="19" cy="12" r="1"/><circle cx="5" cy="12" r="1"/></svg>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const orders = [
  { id: '92834', customer: 'Alex Rivera', avatar: 'https://i.pravatar.cc/150?u=alex', product: 'iPhone 15 Pro', amount: '999.00', status: 'Completed' },
  { id: '92835', customer: 'Sarah Chen', avatar: 'https://i.pravatar.cc/150?u=sarah', product: 'MacBook Air M3', amount: '1,299.00', status: 'Processing' },
  { id: '92836', customer: 'Michael Ross', avatar: 'https://i.pravatar.cc/150?u=michael', product: 'Apple Watch S9', amount: '399.00', status: 'Pending' },
  { id: '92837', customer: 'Elena Gilbert', avatar: 'https://i.pravatar.cc/150?u=elena', product: 'iPad Pro 12.9"', amount: '1,099.00', status: 'Completed' },
  { id: '92838', customer: 'James Wilson', avatar: 'https://i.pravatar.cc/150?u=james', product: 'AirPods Pro 2', amount: '249.00', status: 'Shipped' },
]
</script>

<style scoped>
.table-container {
  padding: 24px;
  width: 100%;
}

.table-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.view-all {
  background: transparent;
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 6px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.85rem;
  transition: all 0.2s;
}

.view-all:hover {
  border-color: var(--text-muted);
  color: var(--text-main);
}

table {
  width: 100%;
  border-collapse: collapse;
}

th {
  text-align: left;
  color: var(--text-muted);
  font-weight: 500;
  font-size: 0.85rem;
  padding: 12px 16px;
  border-bottom: 1px solid var(--border);
}

td {
  padding: 16px;
  border-bottom: 1px solid var(--border);
  font-size: 0.9rem;
}

tr:last-child td {
  border-bottom: none;
}

.id {
  font-weight: 600;
  color: var(--accent);
}

.customer {
  display: flex;
  align-items: center;
  gap: 10px;
}

.customer img {
  width: 32px;
  height: 32px;
  border-radius: 50%;
}

.amount {
  font-weight: 600;
}

.status {
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
}

.status.completed { background: rgba(34, 197, 94, 0.1); color: #22c55e; }
.status.processing { background: rgba(59, 130, 246, 0.1); color: #3b82f6; }
.status.pending { background: rgba(234, 179, 8, 0.1); color: #eab308; }
.status.shipped { background: rgba(168, 85, 247, 0.1); color: #a855f7; }

.action-btn {
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.action-btn:hover {
  color: var(--text-main);
}
</style>
