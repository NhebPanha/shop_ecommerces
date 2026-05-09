<template>
  <div class="chart-widget glass">
    <div class="header">
      <div class="title">
        <h3>Revenue Overview</h3>
        <p>Comparison of this month vs last month</p>
      </div>
      <div class="header-right">
        <div class="legend">
          <div class="legend-item">
            <span class="dot current"></span>
            This Month
          </div>
          <div class="legend-item">
            <span class="dot previous"></span>
            Last Month
          </div>
        </div>
        <div class="time-range">
          <select>
            <option>Last 30 days</option>
            <option>Last 7 days</option>
            <option>Last year</option>
          </select>
        </div>
      </div>
    </div>
    <div class="chart-container">
      <svg viewBox="0 0 1000 350" class="chart" preserveAspectRatio="none">
        <!-- Grid lines -->
        <line x1="0" y1="0" x2="1000" y2="0" stroke="rgba(255,255,255,0.05)" />
        <line x1="0" y1="87" x2="1000" y2="87" stroke="rgba(255,255,255,0.05)" />
        <line x1="0" y1="175" x2="1000" y2="175" stroke="rgba(255,255,255,0.05)" />
        <line x1="0" y1="262" x2="1000" y2="262" stroke="rgba(255,255,255,0.05)" />
        
        <!-- Last Month (Background Line) -->
        <path d="M0,320 C100,300 200,310 300,280 C400,250 500,270 600,240 C700,210 800,230 900,180 C950,150 1000,160 1000,160" fill="none" stroke="var(--text-muted)" stroke-width="2" stroke-dasharray="8,5" opacity="0.4" />

        <!-- This Month (Area) -->
        <path d="M0,300 C100,280 200,320 300,200 C400,80 500,150 600,180 C700,210 800,50 900,100 C950,125 1000,80 1000,80 L1000,350 L0,350 Z" fill="url(#gradient)" opacity="0.2" />
        
        <!-- This Month (Main Line) -->
        <path d="M0,300 C100,280 200,320 300,200 C400,80 500,150 600,180 C700,210 800,50 900,100 C950,125 1000,80 1000,80" fill="none" stroke="var(--accent)" stroke-width="4" stroke-linecap="round" />
        
        <!-- Gradient definition -->
        <defs>
          <linearGradient id="gradient" x1="0%" y1="0%" x2="0%" y2="100%">
            <stop offset="0%" style="stop-color:var(--accent);stop-opacity:0.8" />
            <stop offset="100%" style="stop-color:var(--accent);stop-opacity:0" />
          </linearGradient>
        </defs>
      </svg>
      <div class="labels">
        <span>Mon</span>
        <span>Tue</span>
        <span>Wed</span>
        <span>Thu</span>
        <span>Fri</span>
        <span>Sat</span>
        <span>Sun</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.chart-widget {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 24px;
}

.legend {
  display: flex;
  gap: 16px;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 0.85rem;
  color: var(--text-muted);
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.dot.current { background: var(--accent); box-shadow: 0 0 8px var(--accent-glow); }
.dot.previous { background: var(--text-muted); opacity: 0.5; }

.title h3 {
  font-size: 1.1rem;
  margin-bottom: 4px;
}

.title p {
  font-size: 0.85rem;
  color: var(--text-muted);
}

.time-range select {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  color: var(--text-main);
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 0.85rem;
  outline: none;
}

.chart-container {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.chart {
  width: 100%;
  height: 300px;
}

.labels {
  display: flex;
  justify-content: space-between;
  padding: 12px 10px 0;
  color: var(--text-muted);
  font-size: 0.75rem;
}
</style>
