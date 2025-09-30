<template>
  <div class="py-5" :class="{ 'bg-light': !nightMode, 'bg-dark': nightMode }">
    <div class="container">
      <div class="text-center mb-5" data-aos="fade-down" data-aos-duration="1000">
        <h2 class="display-5 fw-bold">About Me</h2>
        <div class="title-divider"></div>
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
  components: {
    Timeline,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      education: {
        title: "Education",
        data: info.education,
      },
      experience: {
        title: "Experience",
        data: info.experience,
      },
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
</style>