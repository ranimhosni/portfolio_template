<template>
  <section id="about" class="about">
    <div class="about-grid">
      <div class="about-label">
        <span class="label-text">About Me</span>
        <div class="label-line" aria-hidden="true"></div>
      </div>

      <div class="about-image-col">
        <div class="image-frame">
          <img :src="about.image" alt="Profile" class="profile-img" />
          <div class="image-accent" aria-hidden="true"></div>
        </div>
      </div>

      <div class="about-text-col">
        <h2 class="about-heading">
          <span class="heading-thin">About me</span><br />
         
          
        </h2>

        <p class="about-description">{{ about.description }}</p>

        <ul class="highlights" role="list">
          <li
            v-for="(highlight, index) in about.highlights"
            :key="index"
            class="highlight-item"
          >
            <span class="highlight-num" aria-hidden="true">{{ String(index + 1).padStart(2, '0') }}</span>
            <span class="highlight-text">{{ highlight }}</span>
          </li>
        </ul>
      </div>
    </div>

    <div class="marquee-strip" aria-hidden="true">
      <div class="marquee-track">
        <span v-for="n in 8" :key="n" class="marquee-word">Design &nbsp;·&nbsp; Develop &nbsp;·&nbsp; Deliver &nbsp;·&nbsp;</span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',
  props: {
    about: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap');

/* ── Base ── */
.about {
  background: #dde3eb;
  color: #f0ede6;
  padding: 6rem 0 0;
  overflow: hidden;
  font-family: 'DM Sans', sans-serif;
}

/* ── Grid ── */
.about-grid {
  display: grid;
  grid-template-columns: 80px 1fr 1.4fr;
  grid-template-rows: auto;
  gap: 0 3rem;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem 6rem;
  align-items: start;
}

/* ── Label column ── */
.about-label {
  grid-column: 1;
  grid-row: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 0.5rem;
  gap: 1rem;
}

.label-text {
  writing-mode: vertical-rl;
  text-orientation: mixed;
  transform: rotate(180deg);
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: #000000;
}

.label-line {
  flex: 1;
  width: 1px;
  background: linear-gradient(to bottom, #070706 0%, transparent 100%);
  min-height: 80px;
}

/* ── Image column ── */
.about-image-col {
  grid-column: 2;
  grid-row: 1;
  padding-top: 1.5rem;
}

.image-frame {
  position: relative;
  display: inline-block;
}

.profile-img {
  display: block;
  width: 100%;
  max-width: 320px;
  aspect-ratio: 3 / 4;
  object-fit: cover;
  border-radius: 2px;
  filter: grayscale(20%) contrast(1.05);
}

.image-accent {
  position: absolute;
  inset: -10px -10px auto auto;
  width: 60%;
  height: 60%;
  border-top: 1px solid #000000;
  border-right: 1px solid #000000;
  pointer-events: none;
}

/* ── Text column ── */
.about-text-col {
  grid-column: 3;
  grid-row: 1;
  padding-top: 0.5rem;
}

.about-heading {
  font-family: 'Playfair Display', serif;
  line-height: 1.05;
  margin: 0 0 2.5rem;
  letter-spacing: -0.01em;
}

.heading-thin {
  display: block;
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 400;
  font-style: italic;
  color: #000000;
}

.heading-bold {
  display: block;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 700;
  color: #0c0c0c;
}

.heading-outline {
  display: block;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 700;
  color: transparent;
  -webkit-text-stroke: 1.5px #030303;
}

/* ── Description ── */
.about-description {
  font-size: 1rem;
  line-height: 1.85;
  color: #020202;
  margin: 0 0 2.5rem;
  max-width: 480px;
  font-weight: 300;
}

/* ── Highlights ── */
.highlights {
  list-style: none;
  margin: 0;
  padding: 0;
  border-top: 1px solid #1e1e1e;
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  padding: 1rem 0;
  border-bottom: 1px solid #1e1e1e;
  transition: border-color 0.2s;
}

.highlight-item:hover {
  border-bottom-color: #070706;
}

.highlight-num {
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  color: #0a0a09;
  font-variant-numeric: tabular-nums;
  min-width: 1.8rem;
}

.highlight-text {
  font-size: 0.95rem;
  color: #697dd3;
  font-weight: 400;
}

/* ── Marquee ── */
.marquee-strip {
  border-top: 1px solid #1e1e1e;
  overflow: hidden;
  padding: 1rem 0;
}

.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 24s linear infinite;
}

.marquee-word {
  font-family: 'Playfair Display', serif;
  font-size: 0.85rem;
  font-style: italic;
  letter-spacing: 0.08em;
  color: #2e2e2e;
  white-space: nowrap;
  padding-right: 0;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

/* ── Responsive ── */
@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 60px 1fr;
    grid-template-rows: auto auto;
  }

  .about-image-col {
    grid-column: 2;
    grid-row: 1;
  }

  .about-text-col {
    grid-column: 1 / -1;
    grid-row: 2;
    padding-top: 3rem;
  }

  .about-label {
    grid-row: 1;
  }

  .profile-img {
    max-width: 100%;
    aspect-ratio: 4 / 3;
  }
}

@media (max-width: 600px) {
  .about-grid {
    grid-template-columns: 1fr;
    padding: 0 1.25rem 4rem;
  }

  .about-label {
    flex-direction: row;
    align-items: center;
    margin-bottom: 2rem;
  }

  .label-text {
    writing-mode: horizontal-tb;
    transform: none;
  }

  .label-line {
    min-height: unset;
    width: 100%;
    height: 1px;
    background: linear-gradient(to right, #080808 0%, transparent 100%);
  }

  .about-image-col,
  .about-text-col {
    grid-column: 1;
  }
}
</style>