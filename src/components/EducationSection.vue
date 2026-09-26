<template>
  <section id="education" class="education section">
    <div class="container">
      <div class="section-header">
        <span class="section-label">Academic Journey</span>
        <h2 class="section-title">
          <span class="title-accent">Education</span>
        </h2>
        <div class="section-divider"></div>
      </div>

      <div class="education-timeline">
        <div
          v-for="(item, idx) in education"
          :key="idx"
          class="education-card"
          :style="{ animationDelay: `${idx * 0.1}s` }"
        >
          <div class="card-marker">
            <div class="marker-dot"></div>
            <div class="marker-line" v-if="idx < education.length - 1"></div>
          </div>
          
          <div class="card-content">
            <div class="card-header">
              <div class="header-left">
                <h3 class="edu-degree">{{ item.degree }}</h3>
                <div class="edu-institution">
                  <svg class="institution-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M12 3L1 9L12 15L23 9L12 3Z" />
                    <path d="M5 12V16L12 20L19 16V12" />
                  </svg>
                  {{ item.institution }}
                </div>
              </div>
              <div class="edu-dates">
                <svg class="date-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="4" width="18" height="18" rx="2" ry="2" />
                  <line x1="16" y1="2" x2="16" y2="6" />
                  <line x1="8" y1="2" x2="8" y2="6" />
                  <line x1="3" y1="10" x2="21" y2="10" />
                </svg>
                {{ item.dates }}
              </div>
            </div>
            
            <p v-if="item.description" class="edu-description">
              {{ item.description }}
            </p>
            
            <div v-if="item.achievements" class="edu-achievements">
              <div 
                v-for="(achievement, aIdx) in item.achievements" 
                :key="aIdx"
                class="achievement-tag"
              >
                {{ achievement }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'EducationSection',
  props: {
    education: {
      type: Array,
      required: false,
      default: () => []
    }
  }
};
</script>

<style scoped>
.section {
  padding: 5rem 0;
  background: linear-gradient(135deg, #faf9ff 0%, #ffffff 100%);
  position: relative;
  overflow: hidden;
}

.section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg, #697dd3, #8b9ee8, #697dd3);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  position: relative;
  z-index: 1;
}

/* Section Header */
.section-header {
  text-align: center;
  margin-bottom: 3.5rem;
}

.section-label {
  display: inline-block;
  font-size: 0.85rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: #697dd3;
  background: rgba(105, 125, 211, 0.1);
  padding: 0.4rem 1rem;
  border-radius: 20px;
  margin-bottom: 1rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 300;
  margin: 0 0 1rem;
  color: #0c0c0c;
}

.title-accent {
  font-weight: 700;
  background: linear-gradient(135deg, #697dd3, #8b9ee8);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.section-divider {
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #697dd3, transparent);
  margin: 0 auto;
}

/* Timeline Layout */
.education-timeline {
  max-width: 900px;
  margin: 0 auto;
  position: relative;
}

.education-card {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 0;
  position: relative;
  animation: fadeInUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) backwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Timeline Marker */
.card-marker {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  width: 40px;
  flex-shrink: 0;
}

.marker-dot {
  width: 12px;
  height: 12px;
  background: #697dd3;
  border: 3px solid rgba(105, 125, 211, 0.2);
  border-radius: 50%;
  position: relative;
  z-index: 2;
  transition: all 0.3s ease;
}

.education-card:hover .marker-dot {
  transform: scale(1.2);
  background: #8b9ee8;
  border-color: rgba(139, 158, 232, 0.3);
}

.marker-line {
  width: 2px;
  flex: 1;
  background: linear-gradient(180deg, #697dd3, #e0e4f5);
  margin-top: 0.5rem;
}

/* Card Content */
.card-content {
  flex: 1;
  background: white;
  border-radius: 16px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  transition: all 0.3s ease;
  border: 1px solid #f0f2f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
}

.card-content:hover {
  transform: translateX(8px);
  border-color: #e0e4f5;
  box-shadow: 0 8px 24px rgba(105, 125, 211, 0.12);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 1rem;
}

.header-left {
  flex: 1;
}

.edu-degree {
  font-size: 1.25rem;
  font-weight: 700;
  color: #0c0c0c;
  margin: 0 0 0.5rem;
  letter-spacing: -0.3px;
}

.edu-institution {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: #697dd3;
  font-weight: 500;
  background: rgba(105, 125, 211, 0.08);
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
}

.institution-icon,
.date-icon {
  width: 16px;
  height: 16px;
}

.edu-dates {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.85rem;
  color: #6b7280;
  font-weight: 500;
  background: #f9fafb;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  white-space: nowrap;
}

.edu-description {
  margin: 0.75rem 0 0;
  color: #4b5563;
  font-size: 0.95rem;
  line-height: 1.6;
  font-weight: 400;
}

/* Achievements Tags */
.edu-achievements {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 1rem;
}

.achievement-tag {
  font-size: 0.8rem;
  padding: 0.25rem 0.75rem;
  background: #f3f4f6;
  color: #4b5563;
  border-radius: 20px;
  transition: all 0.2s ease;
}

.achievement-tag:hover {
  background: #697dd3;
  color: white;
  transform: translateY(-2px);
}

/* Responsive Design */
@media (max-width: 768px) {
  .section {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .education-card {
    gap: 1rem;
  }

  .card-marker {
    width: 30px;
  }

  .card-content {
    padding: 1.25rem;
    margin-bottom: 1rem;
  }

  .card-header {
    flex-direction: column;
  }

  .edu-dates {
    align-self: flex-start;
  }

  .card-content:hover {
    transform: translateX(4px);
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }

  .edu-degree {
    font-size: 1.1rem;
  }

  .edu-description {
    font-size: 0.9rem;
  }

  .marker-line {
    display: none;
  }

  .card-marker {
    width: 20px;
  }
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
  .section {
    background: linear-gradient(135deg, #1a1a2e, #16213e);
  }

  .section-title {
    color: #ffffff;
  }

  .card-content {
    background: #1f2937;
    border-color: #374151;
  }

  .card-content:hover {
    border-color: #697dd3;
  }

  .edu-degree {
    color: #f3f4f6;
  }

  .edu-description {
    color: #d1d5db;
  }

  .edu-dates {
    background: #374151;
    color: #9ca3af;
  }

  .achievement-tag {
    background: #374151;
    color: #d1d5db;
  }

  .achievement-tag:hover {
    background: #697dd3;
    color: white;
  }
}

/* Print styles */
@media print {
  .section {
    padding: 1rem 0;
    background: white;
  }

  .card-marker,
  .edu-dates svg,
  .institution-icon {
    display: none;
  }

  .card-content {
    box-shadow: none;
    border: 1px solid #ddd;
    page-break-inside: avoid;
  }

  .achievement-tag {
    background: #f0f0f0;
    border: 1px solid #ddd;
  }
}
</style>