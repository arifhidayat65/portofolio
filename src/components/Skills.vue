<template>
  <div class="py-5" :class="{ 'bg-light': !nightMode, 'bg-dark': nightMode }">
    <div class="container">
      <div class="text-center mb-5" data-aos="fade-down" data-aos-duration="1000">
        <h2 class="display-5 fw-bold">Skills</h2>
        <div class="title-divider"></div>
      </div>
      <div class="row g-4">
        <div class="col-lg-4 col-md-6" v-for="(skill, index) in skills" :key="index" data-aos="fade-up" :data-aos-delay="index * 100">
          <div class="skill-card text-center">
            <div class="icon-container mb-3">
              <i :class="skill.icon"></i>
            </div>
            <h3 class="h5 fw-bold">{{ skill.title }}</h3>
            <p class="text-muted">{{ skill.info.join(', ') }}</p>
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
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      skills: info.skills,
    };
  },
};
</script>

<style scoped>
.title-divider {
  width: 100px;
  height: 4px;
  background-color: var(--primary-color);
  margin: 1rem auto;
  border-radius: 2px;
}

.skill-card {
  background-color: var(--surface-color);
  padding: 30px;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  transition: transform 0.3s, box-shadow 0.3s;
  height: 100%;
}

.skill-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 30px rgba(0,0,0,0.15);
}

.icon-container i {
  font-size: 4rem;
  color: var(--primary-color);
  transition: color 0.3s;
}

.skill-card:hover .icon-container i {
    color: var(--secondary-color);
}
</style>