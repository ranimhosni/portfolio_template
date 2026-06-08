<template>
  <header class="header" :class="{ 'is-scrolled': isScrolled }">
    <div class="header-inner">

      <!-- Logo -->
      <a href="#home" class="logo" @click.prevent="handleNavClick('Home')" aria-label="Go to top">
        <span class="logo-mark" aria-hidden="true">HR</span>
        <span class="logo-name">Hosni Ranim</span>
      </a>

      <!-- Desktop nav -->
      <nav class="nav" aria-label="Main navigation">
        <a
          v-for="item in navItems"
          :key="item"
          href="#"
          class="nav-link"
          :class="{ 'nav-link--active': activeItem === item }"
          @click.prevent="handleNavClick(item)"
        >
          {{ item }}
        </a>
      </nav>

      <!-- CTA -->
      <div class="header-actions">
        <a href="#contact" class="cta-btn" @click.prevent="handleNavClick('Contact')">
          Contact Me 
          <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M7 7h10v10"/></svg>
        </a>

        <!-- Mobile toggle -->
        <button
          class="mobile-toggle"
          :class="{ 'is-open': mobileMenuOpen }"
          @click="toggleMobileMenu"
          :aria-expanded="mobileMenuOpen.toString()"
          aria-controls="mobile-nav"
          aria-label="Toggle menu"
        >
          <span class="bar"></span>
          <span class="bar"></span>
        </button>
      </div>

    </div>

    <!-- Mobile nav -->
    <nav
      id="mobile-nav"
      class="mobile-nav"
      :class="{ 'is-open': mobileMenuOpen }"
      aria-label="Mobile navigation"
    >
      <a
        v-for="item in navItems"
        :key="item"
        href="#"
        class="mobile-link"
        :class="{ 'mobile-link--active': activeItem === item }"
        @click.prevent="handleNavClick(item)"
      >
        {{ item }}
      </a>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    navItems: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      isScrolled: false,
      mobileMenuOpen: false,
      activeItem: ''
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50;
    },
    handleNavClick(item) {
      this.activeItem = item;
      this.$emit('scroll-to', item);
      this.mobileMenuOpen = false;
    },
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500&display=swap');

/* ── Variables ── */
.header {
  --purple-a: #667eea;
  --purple-b: #764ba2;
  --border-idle: rgba(102, 126, 234, 0.12);
  --border-scroll: rgba(102, 126, 234, 0.2);
  --text-dark: #1a1625;
  --text-mid: #6b647a;
  --white: #ffffff;
}

/* ── Header shell ── */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  font-family: 'Outfit', sans-serif;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid transparent;
  transition: background 0.3s, border-color 0.3s, box-shadow 0.3s;
}

.header.is-scrolled {
  background: rgba(255, 255, 255, 0.92);
  border-bottom-color: var(--border-scroll);
  box-shadow: 0 1px 24px rgba(102, 126, 234, 0.08);
}

/* ── Inner ── */
.header-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 2rem;
  height: 64px;
  display: flex;
  align-items: center;
  gap: 2rem;
}

/* ── Logo ── */
.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  flex-shrink: 0;
}

.logo-mark {
  width: 34px;
  height: 34px;
  border-radius: 8px;
  background: linear-gradient(135deg, var(--purple-a), var(--purple-b));
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.04em;
  color: #fff;
}

.logo-name {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-dark);
  letter-spacing: -0.01em;
}

/* ── Desktop nav ── */
.nav {
  display: flex;
  align-items: center;
  gap: 0.15rem;
  flex: 1;
  justify-content: center;
}

.nav-link {
  font-size: 0.82rem;
  font-weight: 400;
  color: var(--text-mid);
  text-decoration: none;
  padding: 6px 13px;
  border-radius: 100px;
  transition: color 0.2s, background 0.2s;
  letter-spacing: 0.01em;
}

.nav-link:hover {
  color: var(--text-dark);
  background: rgba(102, 126, 234, 0.07);
}

.nav-link--active {
  color: var(--purple-b);
  background: rgba(102, 126, 234, 0.1);
  font-weight: 500;
}

/* ── Header actions ── */
.header-actions {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  flex-shrink: 0;
}

/* ── CTA button ── */
.cta-btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: 'Outfit', sans-serif;
  font-size: 0.8rem;
  font-weight: 500;
  color: #fff;
  background: linear-gradient(135deg, var(--purple-a), var(--purple-b));
  text-decoration: none;
  padding: 7px 16px;
  border-radius: 100px;
  transition: transform 0.2s, box-shadow 0.2s;
  letter-spacing: 0.02em;
}

.cta-btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 6px 18px rgba(102, 126, 234, 0.35);
}

.cta-btn svg {
  transition: transform 0.2s;
}

.cta-btn:hover svg {
  transform: translate(2px, -2px);
}

/* ── Mobile toggle ── */
.mobile-toggle {
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5px;
  width: 34px;
  height: 34px;
  background: none;
  border: 1px solid var(--border-idle);
  border-radius: 8px;
  cursor: pointer;
  padding: 0;
  transition: border-color 0.2s, background 0.2s;
}

.mobile-toggle:hover {
  background: rgba(102, 126, 234, 0.06);
  border-color: var(--border-scroll);
}

.bar {
  display: block;
  width: 14px;
  height: 1.5px;
  background: var(--text-dark);
  border-radius: 2px;
  transition: transform 0.25s, opacity 0.25s, width 0.25s;
  transform-origin: center;
}

.mobile-toggle.is-open .bar:first-child {
  transform: translateY(3.25px) rotate(45deg);
}

.mobile-toggle.is-open .bar:last-child {
  transform: translateY(-3.25px) rotate(-45deg);
}

/* ── Mobile nav ── */
.mobile-nav {
  display: none;
  flex-direction: column;
  gap: 0;
  padding: 0.5rem 1.5rem 1.25rem;
  border-top: 1px solid var(--border-idle);
  background: rgba(255, 255, 255, 0.96);
  backdrop-filter: blur(16px);
}

.mobile-link {
  font-size: 0.9rem;
  font-weight: 400;
  color: var(--text-mid);
  text-decoration: none;
  padding: 0.75rem 0.5rem;
  border-bottom: 1px solid rgba(102, 126, 234, 0.07);
  transition: color 0.2s;
  letter-spacing: 0.01em;
}

.mobile-link:last-child {
  border-bottom: none;
}

.mobile-link:hover,
.mobile-link--active {
  color: var(--purple-b);
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .nav {
    display: none;
  }

  .mobile-toggle {
    display: flex;
  }

  .mobile-nav {
    display: flex;
  }

  .mobile-nav:not(.is-open) {
    display: none;
  }
}
</style>