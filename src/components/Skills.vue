<template>
  <div class="section skills-section" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="section-header text-center mb-5" data-aos="fade-down" data-aos-duration="700">
        <span class="section-label mono">// skills</span>
        <h2 class="section-title">Technical Skills</h2>
        <div class="title-line"></div>
      </div>
      <div class="row g-4">
        <div
          class="col-lg-4 col-md-6"
          v-for="(skill, index) in skills"
          :key="index"
          data-aos="fade-up"
          :data-aos-delay="index * 80"
        >
          <div class="skill-card">
            <div class="skill-icon-wrap mb-3">
              <i :class="skill.icon"></i>
            </div>
            <h3 class="skill-title">{{ skill.title }}</h3>
            <div class="skill-tags">
              <span class="skill-tag mono" v-for="item in skill.info" :key="item">{{ item }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import info from "../../info";

export default {
  name: "Skills",
  props: {
    nightMode: { type: Boolean },
  },
  data() {
    return {
      skills: info.skills,
    };
  },
};
</script>

<style scoped>
.section {
  background-color: var(--color-primary);
  padding: 80px 0;
}
.section.light-mode { background-color: #F1F5F9; }

.section-label {
  font-size: 0.8rem;
  color: var(--color-accent);
  display: block;
  margin-bottom: 8px;
  letter-spacing: 0.06em;
}
.section.light-mode .section-label { color: #16A34A; }

.section-title {
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  font-weight: 700;
  color: var(--color-foreground);
  margin-bottom: 12px;
}
.section.light-mode .section-title { color: #0F172A; }

.title-line {
  width: 48px;
  height: 3px;
  background: var(--color-accent);
  border-radius: 2px;
  margin: 0 auto;
  box-shadow: 0 0 8px rgba(34, 197, 94, 0.4);
}
.section.light-mode .title-line { box-shadow: none; }

/* Skill card */
.skill-card {
  background-color: var(--color-card);
  border: 1px solid var(--color-border);
  padding: 28px 24px;
  border-radius: var(--border-radius);
  box-shadow: 0 4px 24px rgba(0,0,0,0.3);
  transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease;
  height: 100%;
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.4);
  border-color: var(--color-accent);
}

.section.light-mode .skill-card {
  background-color: #FFFFFF;
  border-color: #E2E8F0;
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
}
.section.light-mode .skill-card:hover {
  border-color: #16A34A;
  box-shadow: 0 8px 24px rgba(0,0,0,0.1);
}

.skill-icon-wrap i {
  font-size: 2.4rem;
  color: var(--color-accent);
  transition: color 0.25s ease, text-shadow 0.25s ease;
}

.skill-card:hover .skill-icon-wrap i {
  text-shadow: 0 0 12px rgba(34, 197, 94, 0.5);
}

.section.light-mode .skill-icon-wrap i { color: #16A34A; }

.skill-title {
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-foreground);
  margin-bottom: 14px;
}
.section.light-mode .skill-title { color: #0F172A; }

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.skill-tag {
  display: inline-block;
  background-color: var(--color-muted);
  color: var(--color-muted-fg);
  border: 1px solid var(--color-border);
  font-size: 0.72rem;
  padding: 3px 8px;
  border-radius: 4px;
  transition: background-color 0.2s ease, color 0.2s ease;
  white-space: nowrap;
}

.skill-card:hover .skill-tag {
  background-color: rgba(34, 197, 94, 0.1);
  color: var(--color-accent);
  border-color: rgba(34, 197, 94, 0.3);
}

.section.light-mode .skill-tag {
  background-color: #F1F5F9;
  color: #475569;
  border-color: #CBD5E1;
}
.section.light-mode .skill-card:hover .skill-tag {
  background-color: #DCFCE7;
  color: #16A34A;
  border-color: #86EFAC;
}
</style>
