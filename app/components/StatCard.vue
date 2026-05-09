<template>
  <div class="stat-card glass">
    <div class="header">
      <div class="icon-box" :style="{ backgroundColor: color + '20', color: color }">
        <slot name="icon"></slot>
      </div>
      <div class="trend" :class="trendUp ? 'up' : 'down'">
        {{ trendValue }}%
        <svg v-if="trendUp" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 6 13.5 15.5 8.5 10.5 1 18"/><polyline points="17 6 23 6 23 12"/></svg>
        <svg v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 18 13.5 8.5 8.5 13.5 1 6"/><polyline points="17 18 23 18 23 12"/></svg>
      </div>
    </div>
    <div class="content">
      <span class="label">{{ label }}</span>
      <h3 class="value">{{ value }}</h3>
    </div>
  </div>
</template>

<script setup>
defineProps({
  label: String,
  value: String,
  trendValue: String,
  trendUp: Boolean,
  color: {
    type: String,
    default: '#3b82f6'
  }
})
</script>

<style scoped>
.stat-card {
  padding: 24px;
  flex: 1;
  min-width: 240px;
  transition: transform 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-5px);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 20px;
}

.icon-box {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.trend {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 0.85rem;
  font-weight: 600;
  padding: 4px 8px;
  border-radius: 20px;
}

.trend.up {
  background: rgba(34, 197, 94, 0.1);
  color: #22c55e;
}

.trend.down {
  background: rgba(239, 68, 68, 0.1);
  color: #ef4444;
}

.content {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.label {
  color: var(--text-muted);
  font-size: 0.9rem;
}

.value {
  font-size: 1.75rem;
  font-weight: 700;
}
</style>
