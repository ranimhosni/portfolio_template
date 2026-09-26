<template>
  <section id="skills" class="skills">
    <div class="container">

      <div class="section-eyebrow">
        <span class="eyebrow-tag">Skills</span>
        <div class="eyebrow-line" aria-hidden="true"></div>
      </div>

      <h2 class="section-heading">What I work with</h2>

      <div class="categories">
        <div
          v-for="category in groupedSkills"
          :key="category.name"
          class="category"
        >
          <div class="category-label">{{ category.name }}</div>
          <div class="pill-row">
            <span
              v-for="skill in category.skills"
              :key="skill.name"
              class="pill"
              :class="'pill--' + skill.category"
            >
              <span class="pill-dot" aria-hidden="true"></span>
              {{ skill.name }}
            </span>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'SkillsSection',
  props: {
    skills: {
      type: Array,
      required: true
    }
  },
  computed: {
    groupedSkills() {
      const map = {};
      const labelMap = {
        frontend: 'Frontend',
        backend: 'Backend',
        database: 'Database',
        tools: 'Tools & DevOps'
      };
      this.skills.forEach(skill => {
        const key = skill.category;
        if (!map[key]) map[key] = { name: labelMap[key] || key, skills: [] };
        map[key].skills.push(skill);
      });
      return Object.values(map);
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500&display=swap');

.skills {
  --purple-a: #667eea;
  --purple-b: #764ba2;
  --dot-fe: #7F77DD;
  --dot-be: #1D9E75;
  --dot-db: #D85A30;
  --dot-tl: #D4537E;
  --fg: #1a1625;
  --fg-muted: #6b647a;
  --border: rgba(118, 75, 162, 0.12);
  --surface: #faf9fc;

  padding: 5rem 2rem;
  background: var(--surface);
  font-family: 'Outfit', sans-serif;
  color: var(--fg);
}

.container {
  max-width: 1100px;
  margin: 0 auto;
}

/* ── Eyebrow ── */
.section-eyebrow {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 2rem;
}

.eyebrow-tag {
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--fg-muted);
  border: 1px solid var(--border);
  padding: 4px 12px;
  border-radius: 100px;
  white-space: nowrap;
}

.eyebrow-line {
  flex: 1;
  height: 1px;
  background: var(--border);
}

/* ── Heading ── */
.section-heading {
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  font-weight: 500;
  color: var(--fg);
  margin: 0 0 3rem;
  letter-spacing: -0.02em;
}

/* ── Categories ── */
.categories {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.category-label {
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--fg-muted);
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 10px;
}

.category-label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--border);
}

/* ── Pills ── */
.pill-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.pill {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 7px 16px;
  border-radius: 100px;
  border: 1px solid var(--border);
  background: #ffffff;
  font-size: 0.85rem;
  font-weight: 400;
  color: var(--fg);
  transition: background 0.15s, border-color 0.15s;
  cursor: default;
}

.pill:hover {
  background: rgba(102, 126, 234, 0.05);
  border-color: rgba(102, 126, 234, 0.25);
}

.pill-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  flex-shrink: 0;
}

.pill--frontend .pill-dot { background: var(--dot-fe); }
.pill--backend  .pill-dot { background: var(--dot-be); }
.pill--database .pill-dot { background: var(--dot-db); }
.pill--tools    .pill-dot { background: var(--dot-tl); }

/* ── Responsive ── */
@media (max-width: 600px) {
  .skills { padding: 3.5rem 1.25rem; }
}
</style>