<template>
  <section id="home" class="hero">
    <div class="hero-bg-grad" aria-hidden="true"></div>
    <div class="hero-orb hero-orb--1" aria-hidden="true"></div>
    <div class="hero-orb hero-orb--2" aria-hidden="true"></div>
    <div class="hero-orb hero-orb--3" aria-hidden="true"></div>
    <div class="hero-grid" aria-hidden="true"></div>
    <canvas class="hero-particles" ref="canvas" aria-hidden="true"></canvas>

    <div class="hero-content">
      <div class="hero-inner" ref="inner">

        <div class="hero-eyebrow animate-up" style="--d:0s">
          <span class="eyebrow-dot"></span>
          <span>Available for work</span>
        </div>

        <h1 class="hero-title animate-up" style="--d:.1s">
          <span class="title-word" v-for="(word, i) in titleWords" :key="i" :style="'--wi:' + i">{{ word }}&nbsp;</span>
        </h1>

        <h2 class="hero-subtitle animate-up" style="--d:.35s">
          <span class="subtitle-shimmer">{{ hero.title }}</span>
        </h2>

        <p class="hero-text animate-up" style="--d:.5s">{{ hero.subtitle }}</p>

        <div class="hero-actions animate-up" style="--d:.65s">
          <button class="btn btn-primary" @click="scrollToProjects">
            {{ hero.cta }}
            <span class="btn-arrow" aria-hidden="true">↗</span>
          </button>
          <div class="resume" @keydown.escape="closeResumeMenu">
            <button class="btn btn-ghost resume-toggle" @click.prevent="toggleResumeMenu" :aria-expanded="resumeMenuOpen.toString()" :aria-label="`Download ${hero.name} resume`">Resume ▾</button>
            <div class="resume-options" v-show="resumeMenuOpen" role="menu" aria-label="Resume options">
              <button class="btn btn-ghost" @click="openResume('fr')" role="menuitem">FR</button>
              <button class="btn btn-ghost" @click="openResume('en')" role="menuitem">EN</button>
            </div>
          </div>
          <a href="https://github.com/ranimhosni" class="btn btn-ghost" target="_blank" rel="noopener noreferrer">GitHub</a>
          <a href="https://www.linkedin.com/in/ranim-hosni-/" class="btn btn-ghost" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        </div>

        <div class="hero-scroll animate-up" style="--d:.85s" aria-hidden="true">
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
    hero: { type: Object, required: true }
  },
  data() {
    return {
      raf: null,
      mouse: { x: 0, y: 0 },
      particles: [],
      particleRaf: null
      ,resumeMenuOpen: false
    };
  },
  computed: {
    titleWords() {
      return this.hero && this.hero.name ? this.hero.name.split(' ') : [];
    }
  },
  mounted() {
    this._root = this.$el;
    this._orb1 = this._root.querySelector('.hero-orb--1');
    this._orb2 = this._root.querySelector('.hero-orb--2');
    this._inner = this.$refs.inner;

    this.onMove = (e) => {
      const r = this._root.getBoundingClientRect();
      this.mouse.x = (e.clientX - r.left) / r.width - 0.5;
      this.mouse.y = (e.clientY - r.top)  / r.height - 0.5;
      if (!this.raf) this.raf = requestAnimationFrame(() => this.applyParallax());
    };
    this.onLeave = () => {
      this.mouse.x = 0; this.mouse.y = 0;
      if (!this.raf) this.raf = requestAnimationFrame(() => this.applyParallax());
    };
    this._root.addEventListener('mousemove', this.onMove);
    this._root.addEventListener('mouseleave', this.onLeave);
    this.initParticles();
  },
  beforeDestroy() {
    if (this.raf) cancelAnimationFrame(this.raf);
    if (this.particleRaf) cancelAnimationFrame(this.particleRaf);
    if (this._root) {
      this._root.removeEventListener('mousemove', this.onMove);
      this._root.removeEventListener('mouseleave', this.onLeave);
    }
  },
  methods: {
    applyParallax() {
      this.raf = null;
      const x = this.mouse.x, y = this.mouse.y;
      if (this._orb1) this._orb1.style.transform = `translate3d(${x*30}px,${y*20}px,0) scale(1.02)`;
      if (this._orb2) this._orb2.style.transform = `translate3d(${x*-18}px,${y*-12}px,0) scale(1.02)`;
      if (this._inner) {
        this._inner.style.transform = `translate3d(${x*-10}px,${y*-8}px,0) rotateX(${y*-4}deg) rotateY(${x*6}deg)`;
      }
    },
    initParticles() {
      const canvas = this.$refs.canvas;
      if (!canvas) return;
      const ctx = canvas.getContext('2d');
      const resize = () => {
        canvas.width  = this._root.offsetWidth;
        canvas.height = this._root.offsetHeight;
      };
      resize();
      window.addEventListener('resize', resize);

      const count = 55;
      this.particles = Array.from({ length: count }, () => ({
        x:  Math.random() * canvas.width,
        y:  Math.random() * canvas.height,
        r:  Math.random() * 1.6 + 0.4,
        vx: (Math.random() - 0.5) * 0.35,
        vy: (Math.random() - 0.5) * 0.35,
        o:  Math.random() * 0.35 + 0.08
      }));

      const draw = () => {
        this.particleRaf = requestAnimationFrame(draw);
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        this.particles.forEach(p => {
          p.x += p.vx; p.y += p.vy;
          if (p.x < 0) p.x = canvas.width;
          if (p.x > canvas.width) p.x = 0;
          if (p.y < 0) p.y = canvas.height;
          if (p.y > canvas.height) p.y = 0;
          ctx.beginPath();
          ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
          ctx.fillStyle = `rgba(255,255,255,${p.o})`;
          ctx.fill();
        });
      };
      draw();
    },
    scrollToProjects() { this.$emit('scroll-to', 'Projects'); },
    toggleResumeMenu() {
      this.resumeMenuOpen = !this.resumeMenuOpen;
    },

    closeResumeMenu() {
      this.resumeMenuOpen = false;
    },

    openResume(lang) {
      // Map language to file paths
      // Open a small HTML wrapper so the page has a favicon (HR) when opened
      const map = {
        fr: '/resume-fr.html',
        en: '/resume-en.html'
      };
      const url = map[lang] || map.fr;
      try {
        window.open(url, '_blank', 'noopener,noreferrer');
      } catch (e) {
        console.warn('Window open failed', e);
      }
      this.closeResumeMenu();
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,600;1,300&family=Outfit:wght@300;400;500&display=swap');

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

  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
  font-family: 'Outfit', sans-serif;
  color: var(--white-full);
  perspective: 1200px;
}

/* ── Layers ── */
.hero-bg-grad {
  position: absolute; inset: 0;
  background: linear-gradient(135deg, var(--purple-a) 0%, var(--purple-b) 100%);
  z-index: 0;
}

.hero-particles {
  position: absolute; inset: 0;
  z-index: 1;
  pointer-events: none;
}

.hero-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  z-index: 2;
  pointer-events: none;
  will-change: transform;
  transition: transform 0.45s cubic-bezier(.2,.9,.3,1);
}

.hero-orb--1 {
  width: 520px; height: 520px;
  top: -130px; right: -110px;
  background: rgba(102,126,234,0.48);
  animation: drift1 14s ease-in-out infinite alternate;
}

.hero-orb--2 {
  width: 400px; height: 400px;
  bottom: -90px; left: -70px;
  background: rgba(118,75,162,0.55);
  animation: drift2 18s ease-in-out infinite alternate;
}

.hero-orb--3 {
  width: 260px; height: 260px;
  top: 40%; left: 20%;
  background: rgba(150,100,220,0.2);
  animation: drift3 22s ease-in-out infinite alternate;
}

@keyframes drift1 { from{transform:translate(0,0)  scale(1)}   to{transform:translate(28px,18px)  scale(1.07)} }
@keyframes drift2 { from{transform:translate(0,0)  scale(1)}   to{transform:translate(-20px,14px) scale(1.05)} }
@keyframes drift3 { from{transform:translate(0,0)  scale(1)}   to{transform:translate(16px,-22px) scale(1.1)}  }

.hero-grid {
  position: absolute; inset: 0; z-index: 3;
  background-image:
    linear-gradient(rgba(255,255,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse 70% 70% at 50% 50%, black 40%, transparent 100%);
}

/* ── Content ── */
.hero-content { position:relative; z-index:4; padding:2rem; width:100%; }

.hero-inner {
  max-width: 780px; margin:0 auto;
  display:flex; flex-direction:column; align-items:center;
  will-change: transform;
  transition: transform 0.35s cubic-bezier(.2,.9,.3,1);
}

/* ── Eyebrow ── */
.hero-eyebrow {
  display:inline-flex; align-items:center; gap:8px;
  font-size:0.7rem; font-weight:500; letter-spacing:0.18em; text-transform:uppercase;
  color:var(--white-55); margin-bottom:1.75rem;
  border:1px solid var(--white-12); padding:6px 16px; border-radius:100px;
  backdrop-filter:blur(8px); background:var(--white-06);
}

.eyebrow-dot {
  width:6px; height:6px; border-radius:50%;
  background:#a8f5b8; box-shadow:0 0 8px #a8f5b8;
  animation:pulse 2s ease-in-out infinite;
}
@keyframes pulse {
  0%,100% { opacity:1; transform:scale(1); }
  50%      { opacity:0.6; transform:scale(0.85); }
}

/* ── Title — word-by-word float in ── */
.hero-title {
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(3.5rem,9vw,7.5rem);
  font-weight:600; line-height:0.95; letter-spacing:-0.02em;
  color:var(--white-full); margin:0 0 1rem;
  display:flex; flex-wrap:wrap; justify-content:center;
}

.title-word {
  display:inline-block;
  animation: wordIn 0.7s cubic-bezier(0.22,1,0.36,1) calc(0.1s + var(--wi,0) * 0.14s) both;
}
@keyframes wordIn {
  from { opacity:0; transform:translateY(36px) rotateX(-20deg); }
  to   { opacity:1; transform:translateY(0)    rotateX(0deg);   }
}

/* ── Subtitle shimmer ── */
.hero-subtitle {
  font-size:clamp(0.95rem,2.5vw,1.2rem); font-weight:300;
  letter-spacing:0.12em; text-transform:uppercase;
  color:var(--white-55); margin:0 0 1.25rem;
  position:relative; display:inline-block;
}
.hero-subtitle::before, .hero-subtitle::after {
  content:''; position:absolute; top:50%; width:28px; height:1px; background:var(--white-30);
}
.hero-subtitle::before { right:calc(100% + 12px); }
.hero-subtitle::after  { left:calc(100% + 12px); }

.subtitle-shimmer {
  position:relative; display:inline-block;
  background:linear-gradient(90deg, var(--white-55) 0%, var(--white-full) 40%, var(--white-55) 80%);
  background-size:200% auto;
  -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  background-clip:text;
  animation:shimmer 4s linear infinite 1.2s;
}
@keyframes shimmer {
  from { background-position:200% center; }
  to   { background-position:-200% center; }
}

/* ── Body text ── */
.hero-text {
  font-size:clamp(0.95rem,2vw,1.1rem); font-weight:300;
  line-height:1.8; color:var(--white-55); max-width:520px; margin:0 0 2.5rem;
}

/* ── Actions ── */
.hero-actions {
  display:flex; align-items:center; gap:1rem;
  flex-wrap:wrap; justify-content:center; margin-bottom:3.5rem;
}

.resume { position: relative; }
.resume-options {
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  display: flex;
  flex-direction: row;
  gap: 8px;
  background: rgba(197, 195, 197, 0.6);
  padding: 8px;
  border-radius: 8px;
  backdrop-filter: blur(6px);
  z-index: 30;
}
.resume-options .btn-ghost { background: transparent; color: var(--white-full); border: 1px solid rgba(94, 91, 91, 0.12); }
.resume-toggle { position: relative; }

.btn {
  display:inline-flex; align-items:center; gap:6px;
  font-family:'Outfit',sans-serif; font-size:0.9rem; font-weight:500;
  padding:0.75rem 1.75rem; border-radius:100px; border:none;
  cursor:pointer; text-decoration:none;
  transition:transform 0.2s, box-shadow 0.2s, background 0.2s;
  letter-spacing:0.02em;
}

.btn-primary { background:var(--white-full); color:var(--purple-b); }
.btn-primary:hover { transform:translateY(-2px); box-shadow:0 12px 32px rgba(0,0,0,0.2); }

.btn-arrow { font-size:1rem; transition:transform 0.2s; }
.btn-primary:hover .btn-arrow { transform:translate(2px,-2px); }

.btn-ghost {
  background:var(--white-12); color:var(--white-85);
  border:1px solid var(--white-12); backdrop-filter:blur(8px);
  position:relative; overflow:hidden;
}
.btn-ghost::after {
  content:''; position:absolute; inset:0;
  background:linear-gradient(120deg, transparent 30%, rgba(255,255,255,0.12) 50%, transparent 70%);
  background-size:200% auto; opacity:0;
  transition:opacity 0.2s;
}
.btn-ghost:hover { background:var(--white-30); transform:translateY(-2px); }
.btn-ghost:hover::after { opacity:1; animation:btnSheen 0.5s linear forwards; }
@keyframes btnSheen {
  from { background-position:200% center; }
  to   { background-position:-200% center; }
}

/* ── Scroll indicator ── */
.hero-scroll { display:flex; flex-direction:column; align-items:center; gap:8px; }
.scroll-line {
  width:1px; height:40px;
  background:linear-gradient(to bottom, var(--white-30), transparent);
  animation:scrollDrop 1.8s ease-in-out infinite;
}
@keyframes scrollDrop {
  0%   { transform:scaleY(0); transform-origin:top;    opacity:1; }
  50%  { transform:scaleY(1); transform-origin:top;    opacity:1; }
  100% { transform:scaleY(1); transform-origin:bottom; opacity:0; }
}
.scroll-label { font-size:0.6rem; letter-spacing:0.2em; text-transform:uppercase; color:var(--white-30); }

/* ── Entrance ── */
.animate-up { animation:slideUp 0.7s cubic-bezier(0.22,1,0.36,1) var(--d,0s) both; }
@keyframes slideUp {
  from { opacity:0; transform:translateY(28px); }
  to   { opacity:1; transform:translateY(0); }
}

/* ── Responsive ── */
@media (max-width:600px) {
  .hero-subtitle::before, .hero-subtitle::after { display:none; }
  .hero-actions { flex-direction:column; width:100%; }
  .btn { width:100%; justify-content:center; }
}
</style>