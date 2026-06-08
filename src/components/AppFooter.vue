<template>
  <footer class="footer">

    <div class="footer-top">
      <div class="footer-brand">
        <span class="brand-initial">HR</span>
        <div class="brand-text">
          <span class="brand-name">Hosni Ranim</span>
          <span class="brand-role">FullStack Developer</span>
        </div>
      </div>

      <nav class="footer-nav" aria-label="Footer navigation">
        <a v-for="item in nav" :key="item" :href="`#${item.toLowerCase()}`" class="footer-link">
          {{ item }}
        </a>
      </nav>

      <div class="footer-social" aria-label="Social links">
        <a
          v-for="link in social"
          :key="link.name"
          :href="link.url"
          target="_blank"
          rel="noopener noreferrer"
          class="social-pill"
          :aria-label="link.name"
        >
          <span class="social-icon" aria-hidden="true">
            <svg v-if="link.name === 'GitHub'" width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
              <path d="M12 .5C5.37.5 0 5.87 0 12.5c0 5.29 3.44 9.77 8.21 11.36.6.11.82-.26.82-.58 0-.29-.01-1.04-.02-2.04-3.34.73-4.04-1.61-4.04-1.61-.55-1.39-1.34-1.76-1.34-1.76-1.09-.75.08-.74.08-.74 1.2.08 1.83 1.23 1.83 1.23 1.07 1.83 2.8 1.3 3.48.99.11-.77.42-1.3.76-1.6-2.66-.3-5.47-1.33-5.47-5.93 0-1.31.47-2.38 1.24-3.22-.12-.3-.54-1.52.12-3.17 0 0 1.01-.32 3.3 1.23a11.5 11.5 0 0 1 3-.4c1.02.01 2.05.14 3 .4 2.28-1.55 3.29-1.23 3.29-1.23.66 1.65.24 2.87.12 3.17.77.84 1.24 1.91 1.24 3.22 0 4.61-2.81 5.62-5.48 5.92.43.37.81 1.1.81 2.22 0 1.6-.02 2.88-.02 3.27 0 .32.22.7.82.58C20.56 22.27 24 17.79 24 12.5 24 5.87 18.63.5 12 .5z"/>
            </svg>
            <svg v-else-if="link.name === 'LinkedIn'" width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
              <path d="M4.98 3.5C4.98 4.88 3.86 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 8h5v16H0zM8 8h4.8v2.2h.1c.7-1.3 2.4-2.2 4-2.2 4.3 0 5.1 2.8 5.1 6.5V24h-5V15.5c0-2.1 0-4.8-3-4.8-3 0-3.5 2.4-3.5 4.6V24H8V8z"/>
            </svg>
            <span v-else>{{ link.icon }}</span>
          </span>
          <span class="social-name">{{ link.name }}</span>
        </a>
      </div>
    </div>

    <div class="footer-bottom">
      <p class="copyright">© {{ currentYear }} Hosni Ranim. </p>
      <div class="status-badge" aria-label="Available for work">
        <span class="status-dot" aria-hidden="true"></span>
        Available for work
      </div>
    </div>

  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  props: {
    social: {
      type: Array,
      required: true
    }
  },
 
  computed: {
    currentYear() {
      return new Date().getFullYear();
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300&family=Outfit:wght@300;400;500&display=swap');

.footer {
   --purple-a: #667eea;
  --purple-b: #764ba2;
  --purple-mid: #6e5bbd;
  --fg: #1a1625;
  --surface: rgba(255,255,255,0.04);
  --border: rgba(255,255,255,0.09);
  --text-dim: rgba(255,255,255,0.38);
  --text-mid: rgba(255,255,255,0.58);
  --text-bright: rgba(255,255,255,0.88);

  background: linear-gradient(145deg, var(--purple-a) 0%, var(--purple-b) 100%);
  font-family: 'Outfit', sans-serif;
  color: var(--text-bright);
  position: relative;
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 48px 48px;
  pointer-events: none;
}

/* ── Top row ── */
.footer-top {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  gap: 2rem;
  max-width: 1100px;
  margin: 0 auto;
  padding: 3.5rem 2rem 2.5rem;
  position: relative;
  z-index: 1;
  border-bottom: 1px solid var(--border);
}

/* ── Brand ── */
.footer-brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

.brand-initial {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  background: rgba(255,255,255,0.12);
  border: 1px solid rgba(255,255,255,0.18);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  color: #fff;
  flex-shrink: 0;
}

.brand-text {
  display: flex;
  flex-direction: column;
  gap: 1px;
}

.brand-name {
  font-size: 0.9rem;
  font-weight: 500;
  color: #fff;
  line-height: 1.2;
}

.brand-role {
  font-size: 0.72rem;
  color: var(--text-mid);
  font-weight: 300;
}

/* ── Nav ── */
.footer-nav {
  display: flex;
  gap: 0.25rem;
}

.footer-link {
  font-size: 0.8rem;
  font-weight: 400;
  color: var(--text-mid);
  text-decoration: none;
  padding: 6px 12px;
  border-radius: 100px;
  transition: color 0.2s, background 0.2s;
  letter-spacing: 0.02em;
}

.footer-link:hover {
  color: #fff;
  background: rgba(255,255,255,0.1);
}

/* ── Social ── */
.footer-social {
  display: flex;
  gap: 0.5rem;
  justify-content: flex-end;
}

.social-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 6px 14px 6px 10px;
  border-radius: 100px;
  background: rgba(255,255,255,0.08);
  border: 1px solid rgba(255,255,255,0.12);
  text-decoration: none;
  color: var(--text-mid);
  font-size: 0.78rem;
  font-weight: 400;
  transition: color 0.2s, background 0.2s, transform 0.2s;
}

.social-pill:hover {
  color: #fff;
  background: rgba(255,255,255,0.16);
  transform: translateY(-2px);
}

.social-icon {
  font-size: 0.95rem;
  line-height: 1;
}

.social-name {
  letter-spacing: 0.02em;
}

/* ── Bottom row ── */
.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1100px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
  position: relative;
  z-index: 1;
}

.copyright {
  font-size: 0.75rem;
  color: var(--text-dim);
  font-weight: 300;
  margin: 0;
}

.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  font-size: 0.72rem;
  font-weight: 400;
  color: var(--text-mid);
  border: 1px solid rgba(255,255,255,0.12);
  padding: 4px 12px;
  border-radius: 100px;
  background: rgba(255,255,255,0.05);
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #a8f5b8;
  box-shadow: 0 0 8px #a8f5b8;
  animation: pulse 2s ease-in-out infinite;
  flex-shrink: 0;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(0.82); }
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .footer-top {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 1.75rem;
  }

  .footer-brand {
    justify-content: center;
  }

  .footer-nav {
    justify-content: center;
    flex-wrap: wrap;
  }

  .footer-social {
    justify-content: center;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 0.75rem;
    text-align: center;
  }
}
</style>