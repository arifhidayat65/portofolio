<template>
  <div id="app" :class="{ 'night-mode': nightMode }">
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
// import Navbar from "./components/Navbar.vue";
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
    // Navbar,
    Home,
    About,
    Skills,
    Portfolio,
    Contact,
    Footer,
  },
  data() {
    return {
      nightMode: false,
      config: info.config,
    };
  },
  created() {
    if (this.config.use_cookies) {
      this.nightMode = this.$cookie.get("nightMode") === "true" ? true : false;
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
:root {
  --background-color: #f4f5f7;
  --surface-color: #ffffff;
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --text-color: #2c3e50;
  --heading-color: #34495e;
  --border-radius: 12px;
  --box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

:root.night-mode {
  --background-color: #1a1a1a;
  --surface-color: #2c2c2c;
  --primary-color: #bb86fc;
  --secondary-color: #03dac6;
  --text-color: #e0e0e0;
  --heading-color: #ffffff;
}

body {
  background-color: var(--background-color);
  color: var(--text-color);
  font-family: "Roboto", sans-serif;
  transition: background-color 0.3s, color 0.3s;
}

#app {
  font-family: "Montserrat", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
}

h1, h2, h3, h4, h5, h6 {
  font-family: "Montserrat", sans-serif;
  color: var(--heading-color);
  font-weight: 700;
}

.parent {
  position: relative;
  padding-top: 60px; /* Adjusted for a fixed navbar */
}

.pgray {
  color: #535a5e;
}

.pblue {
  color: #759CC9;
}

.bg-dark2 {
  background-color: #262c30 !important;
}

.text-light {
  color: #d3d2d2 !important;
}

.p-st {
  transition: all 0.5s !important;
}

/* Modern Scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: var(--surface-color);
}

::-webkit-scrollbar-thumb {
  background-color: var(--primary-color);
  border-radius: 10px;
  border: 2px solid var(--surface-color);
}

::-webkit-scrollbar-thumb:hover {
  background-color: #2980b9;
}

.night-mode ::-webkit-scrollbar-thumb:hover {
  background-color: #9a65d9;
}

/* Tooltip styles - can be refactored later */
.tooltip {
  display: block !important;
  z-index: 10000;
}

.tooltip .tooltip-inner {
  background: var(--heading-color);
  color: var(--background-color);
  border-radius: 8px;
  font-size: 12px;
  padding: 8px 12px;
}

.tooltip .tooltip-arrow {
  border-color: var(--heading-color);
}
</style>