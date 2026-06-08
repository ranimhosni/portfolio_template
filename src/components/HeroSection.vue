<template>
  <section id="home" class="hero">
    <!-- Decorative layers -->
    <div class="hero-bg-grad" aria-hidden="true"></div>
    <div class="hero-orb hero-orb--1" aria-hidden="true"></div>
    <div class="hero-orb hero-orb--2" aria-hidden="true"></div>
    <div class="hero-grid" aria-hidden="true"></div>

    <div class="hero-content">
      <div class="hero-inner">

        <div class="hero-eyebrow animate-up" style="--d:0s">
          <span class="eyebrow-dot"></span>
          <span>Available for work</span>
        </div>

        <h1 class="hero-title animate-up" style="--d:.15s">
          {{ hero.name }}
        </h1>

        <h2 class="hero-subtitle animate-up" style="--d:.3s">
          {{ hero.title }}
        </h2>

        <p class="hero-text animate-up" style="--d:.45s">
          {{ hero.subtitle }}
        </p>

        <div class="hero-actions animate-up" style="--d:.6s">
          <button class="btn btn-primary" @click="scrollToProjects">
            {{ hero.cta }}
            <span class="btn-arrow" aria-hidden="true">↗</span>
          </button>
          <button
            class="btn btn-ghost"
            @click="openAndDownload"
            :aria-label="`Open and download ${hero.name} resume`"
          >
            Resume
          </button>
          <a
            href="https://github.com/ranimhosni"
            class="btn btn-ghost"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Open GitHub profile"
          >
            GitHub
          </a>
          <a
            href="https://www.linkedin.com/in/ranim-hosni-/"
            class="btn btn-ghost"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Open LinkedIn profile"
          >
            LinkedIn
          </a>
        </div>

        <div class="hero-scroll animate-up" style="--d:.8s" aria-hidden="true">
          <div class="scroll-line"></div>
          <span class="scroll-label">scroll</span>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  props: {
    hero: {
      type: Object,
      required: true
    }
  },
  methods: {
    scrollToProjects() {
      this.$emit('scroll-to', 'Projects');
    },
    openAndDownload() {
      const url = this.hero && this.hero.resume ? this.hero.resume : '/CV_Ranim Hosni.pdf';
      try {
        window.open(url, '_blank', 'noopener,noreferrer');
      } catch (e) {
        // fallback: continue to download only
      }

      const link = document.createElement('a');
      link.href = url;
      const fileName = url.split('/').pop() || 'resume.pdf';
      link.setAttribute('download', fileName);
      // some browsers require link to be in document
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,600;1,300&family=Outfit:wght@300;400;500&display=swap');

/* ── Variables ── */
.hero {
  --purple-a: #667eea;
  --purple-b: #764ba2;
  --purple-mid: #7c5cbf;
  --white-full: #ffffff;
  --white-85: rgba(255,255,255,0.85);
  --white-55: rgba(255,255,255,0.55);
  --white-30: rgba(255,255,255,0.30);
  --white-12: rgba(255,255,255,0.12);
  --white-06: rgba(255,255,255,0.06);
}

/* ── Section ── */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
  font-family: 'Outfit', sans-serif;
  color: var(--white-full);
}

/* ── Background layers ── */
.hero-bg-grad {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, var(--purple-a) 0%, var(--purple-b) 100%);
  z-index: 0;
}

.hero-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  z-index: 1;
  pointer-events: none;
}

.hero-orb--1 {
  width: 500px;
  height: 500px;
  top: -120px;
  right: -100px;
  background: rgba(102, 126, 234, 0.5);
  animation: drift 14s ease-in-out infinite alternate;
}

.hero-orb--2 {
  width: 380px;
  height: 380px;
  bottom: -80px;
  left: -60px;
  background: rgba(118, 75, 162, 0.6);
  animation: drift 18s ease-in-out infinite alternate-reverse;
}

@keyframes drift {
  from { transform: translate(0, 0) scale(1); }
  to   { transform: translate(30px, 20px) scale(1.08); }
}

/* ── Grid overlay ── */
.hero-grid {
  position: absolute;
  inset: 0;
  z-index: 2;
  background-image:
    linear-gradient(rgba(255,255,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse 70% 70% at 50% 50%, black 40%, transparent 100%);
}

/* ── Content ── */
.hero-content {
  position: relative;
  z-index: 3;
  padding: 2rem;
  width: 100%;
}

.hero-inner {
  max-width: 780px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
}

/* ── Eyebrow ── */
.hero-eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--white-55);
  margin-bottom: 1.75rem;
  border: 1px solid var(--white-12);
  padding: 6px 16px;
  border-radius: 100px;
  backdrop-filter: blur(8px);
  background: var(--white-06);
}

.eyebrow-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #a8f5b8;
  box-shadow: 0 0 8px #a8f5b8;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(0.85); }
}

/* ── Title ── */
.hero-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(3.5rem, 9vw, 7.5rem);
  font-weight: 600;
  line-height: 0.95;
  letter-spacing: -0.02em;
  color: var(--white-full);
  margin: 0 0 1rem;
}

/* ── Subtitle ── */
.hero-subtitle {
  font-size: clamp(0.95rem, 2.5vw, 1.2rem);
  font-weight: 300;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--white-55);
  margin: 0 0 1.25rem;
  position: relative;
  display: inline-block;
}

.hero-subtitle::before,
.hero-subtitle::after {
  content: '';
  position: absolute;
  top: 50%;
  width: 28px;
  height: 1px;
  background: var(--white-30);
}
.hero-subtitle::before { right: calc(100% + 12px); }
.hero-subtitle::after  { left:  calc(100% + 12px); }

/* ── Body text ── */
.hero-text {
  font-size: clamp(0.95rem, 2vw, 1.1rem);
  font-weight: 300;
  line-height: 1.8;
  color: var(--white-55);
  max-width: 520px;
  margin: 0 0 2.5rem;
}

/* ── Actions ── */
.hero-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 3.5rem;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: 'Outfit', sans-serif;
  font-size: 0.9rem;
  font-weight: 500;
  padding: 0.75rem 1.75rem;
  border-radius: 100px;
  border: none;
  cursor: pointer;
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s, background 0.2s;
  letter-spacing: 0.02em;
}

.btn-primary {
  background: var(--white-full);
  color: var(--purple-b);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 32px rgba(0,0,0,0.2);
}

.btn-arrow {
  font-size: 1rem;
  transition: transform 0.2s;
}

.btn-primary:hover .btn-arrow {
  transform: translate(2px, -2px);
}

.btn-ghost {
  background: var(--white-12);
  color: var(--white-85);
  border: 1px solid var(--white-12);
  backdrop-filter: blur(8px);
}

.btn-ghost:hover {
  background: var(--white-30);
  transform: translateY(-2px);
}

/* ── Scroll indicator ── */
.hero-scroll {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, var(--white-30), transparent);
  animation: scrollDrop 1.8s ease-in-out infinite;
}

@keyframes scrollDrop {
  0%   { transform: scaleY(0); transform-origin: top; opacity: 1; }
  50%  { transform: scaleY(1); transform-origin: top; opacity: 1; }
  100% { transform: scaleY(1); transform-origin: bottom; opacity: 0; }
}

.scroll-label {
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--white-30);
}

/* ── Entrance animation ── */
.animate-up {
  animation: slideUp 0.7s cubic-bezier(0.22, 1, 0.36, 1) var(--d, 0s) both;
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(28px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── Responsive ── */
@media (max-width: 600px) {
  .hero-subtitle::before,
  .hero-subtitle::after { display: none; }

  .hero-actions { flex-direction: column; width: 100%; }
  .btn { width: 100%; justify-content: center; }
}
</style>