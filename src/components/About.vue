<template>
  <div class="section about-section" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="section-header text-center mb-5" data-aos="fade-down" data-aos-duration="700">
        <span class="section-label mono">// about</span>
        <h2 class="section-title">About Me</h2>
        <div class="title-line"></div>
      </div>
      <div class="row g-5">
        <div class="col-md-6">
          <Timeline :data="education" :nightMode="nightMode" />
        </div>
        <div class="col-md-6">
          <Timeline :data="experience" :nightMode="nightMode" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Timeline from "./helpers/Timeline.vue";
import info from "../../info";

export default {
  name: "About",
  components: { Timeline },
  props: {
    nightMode: { type: Boolean },
  },
  data() {
    return {
      education: { title: "Education", data: info.education },
      experience: { title: "Experience", data: info.experience },
    };
  },
};
</script>

<style scoped>
.section {
  background-color: var(--color-background);
  padding: 80px 0;
}
.section.light-mode { background-color: #F8FAFC; }

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
</style>
