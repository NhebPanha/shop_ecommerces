<template>
  <div class="dashboard">
    <div class="welcome">
      <h2>Welcome back, Sam 👋</h2>
      <p>Here's what's happening with your store today.</p>
    </div>

    <div class="stats-grid">
      <StatCard label="Total Revenue" value="$45,231.89" trendValue="20.1" trendUp color="#3b82f6">
        <template #icon>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="12" y1="1" x2="12" y2="23" />
            <path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6" />
          </svg>
        </template>
      </StatCard>

      <StatCard label="Orders" value="+2,350" trendValue="12.5" trendUp color="#a855f7">
        <template #icon>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z" />
            <path d="M3 6h18" />
            <path d="M16 10a4 4 0 0 1-8 0" />
          </svg>
        </template>
      </StatCard>

      <StatCard label="Active Users" value="+12,234" trendValue="18.2" trendUp color="#22c55e">
        <template #icon>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2" />
            <circle cx="9" cy="7" r="4" />
            <path d="M22 21v-2a4 4 0 0 0-3-3.87" />
            <path d="M16 3.13a4 4 0 0 1 0 7.75" />
          </svg>
        </template>
      </StatCard>

      <StatCard label="Bounce Rate" value="42.3%" trendValue="2.1" :trendUp="false" color="#f97316">
        <template #icon>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="m22 2-7 20-4-9-9-4Z" />
            <path d="M22 2 11 13" />
          </svg>
        </template>
      </StatCard>
    </div>

    <div class="content-grid">
      <div class="main-chart">
        <ChartWidget />
      </div>
      <div class="secondary-content">
        <div class="top-products glass">
          <h3>Top Products</h3>
          <div class="product-list">
            <div class="product-item">
              <div class="p-info">
                <span class="p-name">iPhone 15 Pro</span>
                <span class="p-sales">1,234 sales</span>
              </div>
              <span class="p-revenue">$1.2M</span>
            </div>
            <div class="product-item">
              <div class="p-info">
                <span class="p-name">MacBook Air M3</span>
                <span class="p-sales">850 sales</span>
              </div>
              <span class="p-revenue">$1.1M</span>
            </div>
            <div class="product-item">
              <div class="p-info">
                <span class="p-name">iPad Pro</span>
                <span class="p-sales">640 sales</span>
              </div>
              <span class="p-revenue">$700k</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="table-section">
      <OrderTable />
    </div>
  </div>
</template>

<style scoped>
.dashboard {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.welcome h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 4px;
}

.welcome p {
  color: var(--text-muted);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 20px;
}

.content-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

.top-products {
  padding: 24px;
  height: 100%;
}

.top-products h3 {
  margin-bottom: 20px;
  font-size: 1.1rem;
}

.product-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.product-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 12px;
}

.p-info {
  display: flex;
  flex-direction: column;
}

.p-name {
  font-size: 0.95rem;
  font-weight: 600;
}

.p-sales {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.p-revenue {
  font-weight: 700;
  color: var(--accent);
}

@media (max-width: 1280px) {
  .content-grid {
    grid-template-columns: 1fr;
  }
}
</style>
