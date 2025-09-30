<template>
  <nav class="navbar navbar-expand-lg fixed-top p-st" :class="{ 'navbar-scrolled': isScrolled, 'bg-dark': nightMode, 'bg-light': !nightMode }">
    <div class="container">
      <a class="navbar-brand" href="/" @click.prevent="$emit('scroll', 'home')">
        <Logo :nightMode="nightMode" />
      </a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" href="/about" @click.prevent="$emit('scroll', 'about')">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/skills" @click.prevent="$emit('scroll', 'skills')">Skills</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/portfolio" @click.prevent="$emit('scroll', 'portfolio')">Portfolio</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/contact" @click.prevent="$emit('scroll', 'contact')">Contact</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" @click.prevent="switchMode">
              <i :class="['fas', nightMode ? 'fa-sun' : 'fa-moon']" v-tooltip.bottom="nightMode ? 'Light Mode' : 'Night Mode'"></i>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import Logo from "./helpers/Logo.vue";
import info from "../../info";

export default {
  name: "Navbar",
  components: {
    Logo,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      navbarConfig: info.config.navbar,
      isScrolled: false,
    };
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 10;
    },
    switchMode() {
      this.$emit("nightMode", !this.nightMode);
    },
  },
};
</script>

<style scoped>
.navbar {
  transition: background-color 0.3s, box-shadow 0.3s;
  --bs-navbar-nav-link-padding-x: 1rem;
}

.navbar-scrolled {
  background-color: var(--surface-color) !important;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.nav-link {
  font-weight: 500;
  color: var(--text-color);
  transition: color 0.3s;
}

.nav-link:hover {
  color: var(--primary-color);
}

.navbar-toggler {
  border: none;
}

.navbar-toggler:focus {
  box-shadow: none;
}

.navbar-toggler-icon {
  background-image: var(--bs-navbar-toggler-icon-bg);
}

.night-mode .navbar-toggler-icon {
    --bs-navbar-toggler-icon-bg: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba%28255, 255, 255, 0.55%29' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
}
</style>