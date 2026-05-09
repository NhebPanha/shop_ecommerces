<template>
  <aside class="sidebar glass">
    <div class="logo">
      <div class="logo-icon"></div>
      <span>ShopDash</span>
    </div>
    <nav class="nav">
      <NuxtLink to="/" class="nav-item" active-class="active">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="7" height="9" x="3" y="3" rx="1"/><rect width="7" height="5" x="14" y="3" rx="1"/><rect width="7" height="9" x="14" y="12" rx="1"/><rect width="7" height="5" x="3" y="16" rx="1"/></svg>
        Dashboard
      </NuxtLink>
      <NuxtLink to="/products" class="nav-item" active-class="active">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m7.5 4.27 9 5.15"/><path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z"/><path d="m3.3 7 8.7 5 8.7-5"/><path d="M12 22V12"/></svg>
        Products
      </NuxtLink>
      <NuxtLink to="/orders" class="nav-item" active-class="active">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
        Orders
      </NuxtLink>
      <NuxtLink to="/users" class="nav-item" active-class="active">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
        Customers
      </NuxtLink>
    </nav>
    <div class="spacer"></div>
    <div class="nav-item logout">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" x2="9" y1="12" y2="12"/></svg>
      Logout
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 260px;
  height: calc(100vh - 40px);
  position: fixed;
  left: 20px;
  top: 20px;
  display: flex;
  flex-direction: column;
  padding: 24px;
  z-index: 100;
  background: var(--sidebar-bg);
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 40px;
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-main);
}

.logo-icon {
  width: 32px;
  height: 32px;
  background: linear-gradient(135deg, var(--accent), #8b5cf6);
  border-radius: 8px;
  box-shadow: 0 0 15px var(--accent-glow);
}

.nav {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  border-radius: 12px;
  color: var(--text-muted);
  cursor: pointer;
  transition: all 0.2s ease;
  font-weight: 500;
}

.nav-item:hover {
  color: var(--text-main);
  background: rgba(0, 0, 0, 0.04);
}

@media (prefers-color-scheme: dark) {
  .nav-item:hover {
    background: rgba(255, 255, 255, 0.05);
  }
}

.nav-item.active {
  color: var(--text-main);
  background: var(--accent);
  box-shadow: 0 4px 15px var(--accent-glow);
}

.nav-item svg {
  opacity: 0.8;
}

.spacer {
  flex: 1;
}

.logout {
  margin-top: auto;
}
</style>
