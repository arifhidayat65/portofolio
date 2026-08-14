<template>
  <div>
    <nav
      class="navbar navbar-expand-lg fixed-top p-st"
      :class="{ 'light-mode': !nightMode, 'navbar-blur': navbarConfig.blur }"
    >
      <div class="container">
        <a
          class="navbar-brand"
          href="/"
          @click.prevent="$emit('scroll', 'home')"
        >
          <Logo :nightMode="nightMode" />
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <i class="fas fa-bars"></i>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="nav ms-auto align-items-center gap-1" role="tablist">
            <li class="nav-item">
              <a
                class="nav-link"
                href="/about"
                @click.prevent="$emit('scroll', 'about')"
              >About</a>
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                href="/skills"
                @click.prevent="$emit('scroll', 'skills')"
              >Skills</a>
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                href="/portfolio"
                @click.prevent="$emit('scroll', 'portfolio')"
              >Portfolio</a>
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                href="/contact"
                @click.prevent="$emit('scroll', 'contact')"
              >Contact</a>
            </li>
            <li class="nav-item ms-2">
              <button
                class="mode-btn"
                @click="switchMode"
                :aria-label="nightMode ? 'Switch to Light Mode' : 'Switch to Dark Mode'"
                v-tooltip.bottom="nightMode ? 'Light Mode' : 'Dark Mode'"
              >
                <i :class="nightMode ? 'fas fa-sun' : 'fas fa-moon'"></i>
              </button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import Logo from "./helpers/Logo";
import info from "../../info";

export default {
  name: "Navbar",
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      navbarConfig: info.config.navbar,
      localNightMode: this.nightMode,
    };
  },
  components: {
    Logo,
  },
  methods: {
    switchMode() {
      this.localNightMode = !this.localNightMode;
      this.$emit("nightMode", this.localNightMode);
    },
  },
};
</script>

<style scoped>
nav {
  background-color: rgba(15, 23, 42, 0.85);
  border-bottom: 1px solid rgba(71, 85, 105, 0.4);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
}

nav.light-mode {
  background-color: rgba(241, 245, 249, 0.85);
  border-bottom: 1px solid rgba(203, 213, 225, 0.6);
}

.navbar-brand { color: var(--color-accent) !important; }

.nav-link {
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--color-muted-fg);
  padding: 6px 12px;
  border-radius: 6px;
  transition: color 0.15s ease, background-color 0.15s ease;
  cursor: pointer;
}

.nav-link:hover {
  color: var(--color-foreground);
  background-color: var(--color-muted);
}

nav.light-mode .nav-link { color: #64748B; }
nav.light-mode .nav-link:hover { color: #0F172A; background-color: #E2E8F0; }

.mode-btn {
  background: var(--color-muted);
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
  border-radius: 8px;
  width: 36px;
  height: 36px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background-color 0.15s ease, color 0.15s ease, border-color 0.15s ease;
  outline: none;
}

.mode-btn:hover {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border-color: var(--color-accent);
}

.mode-btn:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

nav.light-mode .mode-btn {
  background: #E2E8F0;
  border-color: #CBD5E1;
  color: #475569;
}

.navbar-toggler {
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
  border-radius: 8px;
  padding: 6px 10px;
  background: var(--color-muted);
}

/* Responsive: show navbar collapse on mobile */
@media (max-width: 991px) {
  .collapse.navbar-collapse.show {
    background-color: var(--color-primary);
    border-radius: 8px;
    padding: 12px;
    margin-top: 8px;
  }
  nav.light-mode .collapse.navbar-collapse.show {
    background-color: #E2E8F0;
  }
}
</style>
