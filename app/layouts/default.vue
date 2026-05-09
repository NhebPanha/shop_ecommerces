<template>
  <div class="layout">
    <Sidebar />
    <main class="main-content">
      <Header />
      <div class="page-container">
        <slot />
      </div>
    </main>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  min-height: 100vh;
  background-color: var(--bg-main);
  background-image: 
    radial-gradient(at 0% 0%, var(--accent-glow) 0, transparent 50%), 
    radial-gradient(at 50% 0%, rgba(139, 92, 246, 0.05) 0, transparent 50%);
}

.main-content {
  flex: 1;
  margin-left: 300px;
  padding: 20px 40px 40px 20px;
  min-height: 100vh;
}

.page-container {
  max-width: 1400px;
  margin: 0 auto;
}

@media (max-width: 1024px) {
  .main-content {
    margin-left: 0;
    padding: 20px;
  }
}
</style>
