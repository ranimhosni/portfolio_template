<template>
  <section id="softside" class="softside">
    <div class="softside-inner">
      <div class="section-header">
        <span class="section-tag">Community & Growth</span>
        <h2 class="section-heading">Associative life / <span class="highlight">Soft Side</span></h2>
        <div class="heading-underline"></div>
      </div>

      <div class="soft-list">
        <div v-if="soft && soft.items && soft.items.length" class="items-container">
          <ul>
            <li v-for="(item, idx) in soft.items" :key="idx">
              <span class="list-marker">✦</span>
              {{ item }}
            </li>
          </ul>
          <div v-if="soft && soft.instagram" class="soft-links">
            <a :href="soft.instagram" class="soft-link" target="_blank" rel="noopener noreferrer">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true" style="margin-right:8px;">
                <path d="M7 2C4.24 2 2 4.24 2 7v10c0 2.76 2.24 5 5 5h10c2.76 0 5-2.24 5-5V7c0-2.76-2.24-5-5-5H7zm10 2a3 3 0 0 1 3 3v10a3 3 0 0 1-3 3H7a3 3 0 0 1-3-3V7a3 3 0 0 1 3-3h10zM12 7.5a4.5 4.5 0 1 0 0 9 4.5 4.5 0 0 0 0-9zm0 2a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5zM17.7 6.3a1.1 1.1 0 1 1-2.2 0 1.1 1.1 0 0 1 2.2 0z"/>
              </svg>
              Visit Riri's Candles on Instagram
            </a>
          </div>
        </div>
        <div v-else class="empty-state">
          <div class="empty-icon">🌱</div>
          <p>No entries yet — add associative activities or soft-skills here.</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SoftSide',
  props: {
    soft: {
      type: Object,
      required: false,
      default: () => ({ items: [] })
    }
  }
};
</script>

<style scoped>
.softside {
  padding: 5rem 2rem;
  background: linear-gradient(135deg, #faf9ff 0%, #f5f3ff 100%);
  border-radius: 2rem;
  margin: 2rem 0;
}

.softside-inner {
  max-width: 800px;
  margin: 0 auto;
}

/* Header section */
.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-tag {
  display: inline-block;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 600;
  color: #7c6e9e;
  background: rgba(124, 110, 158, 0.1);
  padding: 0.3rem 1rem;
  border-radius: 30px;
  margin-bottom: 1rem;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
}

.section-heading {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(2rem, 5vw, 3.2rem);
  font-weight: 600;
  margin: 0.5rem 0 1rem;
  color: #1a102c;
  letter-spacing: -0.01em;
}

.section-heading .highlight {
  background: linear-gradient(120deg, #8b7bb5, #5e4b8b);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

.heading-underline {
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #8b7bb5, #c7b9ff);
  margin: 1rem auto 0;
  border-radius: 3px;
}

/* List styling */
.items-container ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.9rem;
}

.items-container li {
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  font-size: 1.05rem;
  background: white;
  padding: 0.9rem 1.5rem;
  border-radius: 60px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.02), 0 1px 2px rgba(0, 0, 0, 0.03);
  transition: all 0.25s ease;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  border: 1px solid rgba(124, 110, 158, 0.15);
  backdrop-filter: blur(2px);
}

.items-container li:hover {
  transform: translateX(8px);
  border-color: rgba(124, 110, 158, 0.3);
  box-shadow: 0 10px 20px -8px rgba(0, 0, 0, 0.1);
}

.soft-links { margin-top: 1.25rem; display:flex; justify-content:center; }
.soft-link { display:inline-flex; align-items:center; gap:6px; padding:0.6rem 1rem; background:#f7eefc; color:#5e4b8b; border-radius:999px; text-decoration:none; font-weight:600; border:1px solid rgba(94,75,139,0.12); }
.soft-link:hover { transform:translateY(-3px); box-shadow:0 8px 20px rgba(94,75,139,0.08); }

.list-marker {
  font-size: 1.2rem;
  color: #7c6e9e;
  font-weight: 500;
  display: inline-block;
  width: 1.5rem;
}

/* Empty state */
.empty-state {
  text-align: center;
  padding: 3rem 2rem;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 2rem;
  border: 1px dashed rgba(124, 110, 158, 0.3);
}

.empty-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  opacity: 0.6;
}

.empty-state p {
  color: #4a3f66;
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.95rem;
  margin: 0;
}

/* Responsive */
@media (max-width: 640px) {
  .softside {
    padding: 3rem 1rem;
    margin: 1rem 0;
  }

  .items-container li {
    font-size: 0.95rem;
    padding: 0.7rem 1rem;
  }

  .list-marker {
    font-size: 1rem;
    width: 1.2rem;
  }
}
</style>