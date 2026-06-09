<template>
  <section id="projects" class="projects">
    <div class="container">
      <h2 class="section-title">Projects</h2>
      <div class="projects-grid">
        <div 
          v-for="project in projects" 
          :key="project.id"
          class="project-card"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
            <div class="project-overlay">
              <a :href="project.github" target="_blank" class="project-link">GitHub</a>
              <a :href="project.demo" target="_blank" class="project-link">Demo</a>
            </div>
          </div>
          <div class="project-content">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-tags">
              <span 
                v-for="tag in project.tags" 
                :key="tag"
                class="tag"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',
  props: {
    projects: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
.projects {
  padding: 5rem 2rem;
  background: transparent;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  position: relative;
  text-align: center;
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  letter-spacing: -1px;
  color: #1f2937;
  margin-bottom: 4rem;
  padding-bottom: 1rem;
  line-height: 1.2;
}

.section-title::after {
  content: "";
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(-50%);
  width: 70px;
  height: 4px;
  border-radius: 999px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.project-card {
  background: var(--card-bg);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(46, 49, 55, 0.06);
  border: 1px solid rgba(44,62,80,0.04);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.project-image {
  position: relative;
  overflow: hidden;
  height: 200px;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(180deg, rgba(0,0,0,0.24), rgba(0,0,0,0.6));
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  opacity: 0;
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-link {
  padding: 0.5rem 1rem;
  background: rgba(255,255,255,0.95);
  color: #2c3e50;
  text-decoration: none;
  border-radius: 999px;
  font-weight: 700;
  letter-spacing: 0.2px;
  transition: transform 0.18s ease, background 0.18s ease;
}

.project-link:hover {
  background: #3498db;
  color: white;
}

.project-content {
  padding: 1.5rem;
}

.project-content h3 {
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.project-content p {
  color: #7f8c8d;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  padding: 0.25rem 0.75rem;
  background: #ecf0f1;
  color: #2c3e50;
  border-radius: 15px;
  font-size: 0.85rem;
}
</style>