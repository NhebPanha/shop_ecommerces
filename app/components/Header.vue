<template>
  <header class="header glass">
    <div class="search">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
      <input type="text" placeholder="Search analytics, orders..." />
    </div>
    <div class="actions">
      <button class="icon-btn theme-toggle" @click="toggleTheme" title="Toggle Theme">
        <svg v-if="isDark" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="4"/><path d="M12 2v2"/><path d="M12 20v2"/><path d="m4.93 4.93 1.41 1.41"/><path d="m17.66 17.66 1.41 1.41"/><path d="M2 12h2"/><path d="M20 12h2"/><path d="m6.34 17.66-1.41 1.41"/><path d="m19.07 4.93-1.41 1.41"/></svg>
        <svg v-else xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"/></svg>
      </button>
      <button class="icon-btn">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 8a6 6 0 0 1 12 0c0 7 3 9 3 9H3s3-2 3-9"/><path d="M10.3 21a1.94 1.94 0 0 0 3.4 0"/></svg>
        <span class="badge"></span>
      </button>
      <div class="user">
        <div class="user-info">
          <span class="name">Sam Leang</span>
          <span class="role">Administrator</span>
        </div>
        <div class="avatar">
          <img src="https://ui-avatars.com/api/?name=Sam+Leang&background=3b82f6&color=fff" alt="Avatar" />
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
const isDark = ref(false)

onMounted(() => {
  // Check if user has a preference in localStorage or system
  const savedTheme = localStorage.getItem('theme')
  const systemDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  
  if (savedTheme === 'dark' || (!savedTheme && systemDark)) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  } else if (savedTheme === 'light') {
    isDark.value = false
    document.documentElement.classList.add('light')
  }
})

function toggleTheme() {
  isDark.value = !isDark.value
  if (isDark.value) {
    document.documentElement.classList.remove('light')
    document.documentElement.classList.add('dark')
    localStorage.setItem('theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    document.documentElement.classList.add('light')
    localStorage.setItem('theme', 'light')
  }
}
</script>

<style scoped>
.header {
  height: 70px;
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
}

.search {
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(0, 0, 0, 0.03);
  padding: 8px 16px;
  border-radius: 12px;
  width: 400px;
  border: 1px solid var(--border);
}

@media (prefers-color-scheme: dark) {
  .search {
    background: rgba(255, 255, 255, 0.05);
  }
}

.search input {
  background: transparent;
  border: none;
  color: var(--text-main);
  outline: none;
  width: 100%;
  font-family: inherit;
}

.search svg {
  color: var(--text-muted);
}

.actions {
  display: flex;
  align-items: center;
  gap: 20px;
}

.icon-btn {
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 10px;
  transition: all 0.2s ease;
}

.icon-btn:hover {
  background: rgba(0, 0, 0, 0.04);
  color: var(--text-main);
}

@media (prefers-color-scheme: dark) {
  .icon-btn:hover {
    background: rgba(255, 255, 255, 0.05);
  }
}

.theme-toggle svg {
  transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.theme-toggle:hover svg {
  transform: rotate(15deg);
}

.badge {
  position: absolute;
  top: -2px;
  right: -2px;
  width: 8px;
  height: 8px;
  background: #ef4444;
  border-radius: 50%;
  border: 2px solid var(--bg-dark);
}

.user {
  display: flex;
  align-items: center;
  gap: 12px;
  padding-left: 20px;
  border-left: 1px solid var(--border);
}

.user-info {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.name {
  font-size: 0.9rem;
  font-weight: 600;
}

.role {
  font-size: 0.75rem;
  color: var(--text-muted);
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  overflow: hidden;
  border: 2px solid var(--border);
}

.avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
