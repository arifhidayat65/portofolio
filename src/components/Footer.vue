<template>
  <footer class="footer" :class="{ 'night-mode': nightMode }">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-md-6 text-center text-md-start mb-3 mb-md-0">
          <span>© {{ new Date().getFullYear() }} Copyright: Arif Hidayat</span>
        </div>
        <div class="col-md-6 text-center text-md-end">
          <a :href="linkedin" target="_blank" class="social-icon me-3" v-tooltip.top="'LinkedIn'"><i class="fab fa-linkedin"></i></a>
          <a :href="github" target="_blank" class="social-icon me-3" v-tooltip.top="'GitHub'"><i class="fab fa-github"></i></a>
          <a :href="twitter" target="_blank" class="social-icon me-3" v-tooltip.top="'Twitter'"><i class="fab fa-twitter"></i></a>
          <a :href="facebook" target="_blank" class="social-icon" v-tooltip.top="'Facebook'"><i class="fab fa-facebook"></i></a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import info from "../../info";

export default {
  name: "Footer",
  props: {
    nightMode: Boolean,
  },
  data() {
    return {
      linkedin: info.links.linkedin,
      github: info.links.github,
      facebook: info.links.facebook,
      twitter: info.links.twitter,
    };
  },
};
</script>

<style scoped>
.footer {
  background-color: var(--surface-color);
  padding: 2rem 0;
  color: var(--text-color);
  border-top: 1px solid #dee2e6;
}

.night-mode .footer {
    border-top-color: #4d4d4d;
}

.social-icon {
  color: var(--text-color);
  font-size: 1.5rem;
  transition: color 0.3s;
}

.social-icon:hover {
  color: var(--primary-color);
}
</style>