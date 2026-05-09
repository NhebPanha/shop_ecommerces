<template>
  <div class="auth-layout">
    <div class="auth-container">
      <div class="auth-card glass">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.auth-layout {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--bg-main);
  background-image: 
    radial-gradient(at 0% 0%, var(--accent-glow) 0, transparent 50%), 
    radial-gradient(at 100% 100%, rgba(139, 92, 246, 0.1) 0, transparent 50%);
}

.auth-container {
  width: 100%;
  max-width: 450px;
  padding: 20px;
}

.auth-card {
  padding: 40px;
  border-radius: 24px;
}
</style>
