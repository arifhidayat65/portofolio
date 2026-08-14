<template>
  <div id="app" :class="{ 'light-mode': !nightMode }">
    <Navbar @scroll="scrollTo" @nightMode="switchMode" :nightMode="nightMode" />
    <div class="parent">
      <Home :nightMode="nightMode" />
      <About id="about" :nightMode="nightMode" />
      <Skills id="skills" :nightMode="nightMode" />
      <Portfolio id="portfolio" :nightMode="nightMode" />
      <Contact id="contact" :nightMode="nightMode" />
      <Footer :nightMode="nightMode" />
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Home from "./components/Home";
import About from "./components/About";
import Skills from "./components/Skills";
import Portfolio from "./components/Portfolio";
import Contact from "./components/Contact";
import Footer from "./components/Footer";

import info from "../info";

export default {
  name: "App",
  components: {
    Navbar,
    Home,
    About,
    Skills,
    Portfolio,
    Contact,
    Footer,
  },
  data() {
    return {
      nightMode: true,
      config: info.config,
    };
  },
  created() {
    if (this.config.use_cookies) {
      const saved = this.$cookie.get("nightMode");
      // null = no cookie yet → keep default (dark mode)
      if (saved !== null) {
        this.nightMode = saved === "true";
      }
    }
  },
  mounted() {
    ["about", "contact", "skills", "portfolio"].forEach((l) => {
      if (window.location.href.includes(l)) {
        var elementPosition = document.getElementById(l).offsetTop;
        window.scrollTo({ top: elementPosition - 35, behavior: "smooth" });
      }
    });
  },
  methods: {
    switchMode(mode) {
      if (this.config.use_cookies) {
        this.$cookie.set("nightMode", mode);
      }
      this.nightMode = mode;
    },
    scrollTo(ele) {
      if (ele == "home") {
        this.$router.push(`/`).catch(()=>{});
        window.scrollTo({ top: -80, behavior: "smooth" });
      } else {
        var elementPosition = document.getElementById(ele).offsetTop;
        window.scrollTo({ top: elementPosition - 35, behavior: "smooth" });
        if (this.$router.history.current.path !== `/${ele}`)
          this.$router.push(`/${ele}`);
      }
    },
  },
};
</script>

<style>
/* ==========================================================
   UI UX Pro Max — Dark Mode (OLED) Design System
   Generated: software engineer portfolio
   Style: Dark Mode (OLED) | Accent: #22C55E green
   Fonts: IBM Plex Sans (body) / JetBrains Mono (code)
   ========================================================== */

/* Dark mode (OLED) — DEFAULT */
:root {
  --color-background:    #0F172A;
  --color-foreground:    #F8FAFC;
  --color-primary:       #1E293B;
  --color-on-primary:    #F8FAFC;
  --color-secondary:     #334155;
  --color-on-secondary:  #F8FAFC;
  --color-accent:        #22C55E;
  --color-on-accent:     #0F172A;
  --color-card:          #1B2336;
  --color-card-fg:       #F8FAFC;
  --color-muted:         #272F42;
  --color-muted-fg:      #94A3B8;
  --color-border:        #475569;
  --color-destructive:   #EF4444;
  --color-ring:          #22C55E;

  /* Legacy aliases used by existing components */
  --background-color:  var(--color-background);
  --surface-color:     var(--color-card);
  --primary-color:     var(--color-accent);
  --secondary-color:   #38BDF8;
  --text-color:        var(--color-foreground);
  --heading-color:     #FFFFFF;
  --border-radius:     12px;
  --box-shadow:        0 4px 24px rgba(0, 0, 0, 0.5);
}

/* Light mode override */
:root.light-mode,
body.light-mode {
  --color-background:    #F1F5F9;
  --color-foreground:    #0F172A;
  --color-primary:       #E2E8F0;
  --color-on-primary:    #0F172A;
  --color-secondary:     #CBD5E1;
  --color-on-secondary:  #0F172A;
  --color-accent:        #16A34A;
  --color-on-accent:     #FFFFFF;
  --color-card:          #FFFFFF;
  --color-card-fg:       #0F172A;
  --color-muted:         #E2E8F0;
  --color-muted-fg:      #64748B;
  --color-border:        #CBD5E1;

  --background-color:  var(--color-background);
  --surface-color:     var(--color-card);
  --primary-color:     var(--color-accent);
  --secondary-color:   #0284C7;
  --text-color:        var(--color-foreground);
  --heading-color:     #0F172A;
  --box-shadow:        0 4px 20px rgba(0, 0, 0, 0.08);
}

/* Base */
html { color-scheme: dark; }
body.light-mode { color-scheme: light; }

body {
  background-color: var(--color-background);
  color: var(--color-foreground);
  font-family: "IBM Plex Sans", system-ui, -apple-system, sans-serif;
  font-size: 16px;
  line-height: 1.6;
  transition: background-color 0.25s ease, color 0.25s ease;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  width: 100%;
  min-height: 100vh;
  background-color: var(--color-background);
}

/* Typography */
h1, h2, h3, h4, h5, h6 {
  font-family: "IBM Plex Sans", system-ui, sans-serif;
  color: var(--heading-color);
  font-weight: 700;
  letter-spacing: -0.02em;
}

code, pre, .mono {
  font-family: "JetBrains Mono", "Fira Code", monospace;
  font-size: 0.9em;
}

/* Layout */
.parent {
  position: relative;
  padding-top: 60px;
}

/* Utility overrides */
.bg-dark2  { background-color: var(--color-primary) !important; }
.text-light { color: var(--color-muted-fg) !important; }
.p-st { transition: all 0.25s ease !important; }

/* Minimal green glow effect (key effect from design system) */
.glow {
  text-shadow: 0 0 10px rgba(34, 197, 94, 0.4);
}

/* Scrollbar */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(--color-primary); }
::-webkit-scrollbar-thumb {
  background-color: var(--color-border);
  border-radius: 3px;
}
::-webkit-scrollbar-thumb:hover { background-color: var(--color-accent); }

/* Focus — keyboard nav (WCAG AA) */
:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 3px;
}

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

/* Tooltip */
.tooltip {
  display: block !important;
  z-index: 10000;
}
.tooltip .tooltip-inner {
  background: var(--color-secondary);
  color: var(--color-foreground);
  border-radius: 6px;
  font-size: 12px;
  padding: 6px 10px;
}
.tooltip .tooltip-arrow { border-color: var(--color-secondary); }
</style>