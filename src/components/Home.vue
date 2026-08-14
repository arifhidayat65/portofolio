<template>
  <div class="hero" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="row align-items-center min-vh-hero">
        <!-- Profile picture -->
        <div class="col-md-5 text-center mb-5 mb-md-0" data-aos="fade-right" data-aos-duration="800">
          <div class="avatar-wrapper">
            <img :src="picture" class="profile-picture" alt="Arif Hidayat — Software Engineer">
            <div class="avatar-ring"></div>
          </div>
        </div>
        <!-- Content -->
        <div class="col-md-7" data-aos="fade-left" data-aos-duration="800" data-aos-delay="100">
          <div class="hero-badge mb-3">
            <span class="mono">// software engineer</span>
          </div>
          <h1 class="hero-title">
            Hi, I'm <span class="accent">Arif Hidayat</span>
          </h1>
          <p class="hero-desc" v-html="description"></p>
          <div class="social-row mt-4">
            <a :href="linkedin" target="_blank" rel="noopener" class="social-btn" aria-label="LinkedIn" v-tooltip.bottom="'LinkedIn'">
              <i class="fab fa-linkedin-in"></i>
            </a>
            <a :href="github" target="_blank" rel="noopener" class="social-btn" aria-label="GitHub" v-tooltip.bottom="'GitHub'">
              <i class="fab fa-github"></i>
            </a>
            <a :href="twitter" target="_blank" rel="noopener" class="social-btn" aria-label="Twitter" v-tooltip.bottom="'Twitter'">
              <i class="fab fa-twitter"></i>
            </a>
            <a :href="facebook" target="_blank" rel="noopener" class="social-btn" aria-label="Facebook" v-tooltip.bottom="'Facebook'">
              <i class="fab fa-facebook-f"></i>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import info from "../../info";

export default {
  name: "Home",
  props: {
    nightMode: { type: Boolean },
  },
  data() {
    return {
      picture: info.flat_picture,
      description: info.description,
      linkedin: info.links.linkedin,
      github: info.links.github,
      twitter: info.links.twitter,
      facebook: info.links.facebook,
    };
  },
};
</script>

<style scoped>
.hero {
  background-color: var(--color-background);
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 80px 0 60px;
}

.hero.light-mode { background-color: #F1F5F9; }

.min-vh-hero { min-height: calc(100vh - 140px); }

/* Avatar */
.avatar-wrapper {
  position: relative;
  display: inline-block;
}

.profile-picture {
  width: 260px;
  height: 260px;
  object-fit: cover;
  border-radius: 50%;
  border: 3px solid var(--color-accent);
  box-shadow: 0 0 40px rgba(34, 197, 94, 0.2), 0 20px 60px rgba(0,0,0,0.4);
  position: relative;
  z-index: 1;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.profile-picture:hover {
  transform: translateY(-4px);
  box-shadow: 0 0 60px rgba(34, 197, 94, 0.3), 0 30px 70px rgba(0,0,0,0.4);
}

.avatar-ring {
  position: absolute;
  inset: -8px;
  border-radius: 50%;
  border: 1px dashed rgba(34, 197, 94, 0.3);
  animation: spin 20s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }

@media (prefers-reduced-motion: reduce) {
  .avatar-ring { animation: none; }
}

/* Text */
.hero-badge {
  display: inline-block;
  background-color: var(--color-muted);
  border: 1px solid var(--color-border);
  border-radius: 6px;
  padding: 4px 12px;
  font-size: 0.8rem;
  color: var(--color-accent);
  letter-spacing: 0.05em;
}

.hero.light-mode .hero-badge {
  background-color: #DCFCE7;
  border-color: #86EFAC;
  color: #16A34A;
}

.hero-title {
  font-size: clamp(2rem, 5vw, 3.2rem);
  font-weight: 700;
  color: var(--color-foreground);
  line-height: 1.15;
  margin-bottom: 1rem;
}

.hero.light-mode .hero-title { color: #0F172A; }

.accent {
  color: var(--color-accent);
  text-shadow: 0 0 20px rgba(34, 197, 94, 0.3);
}

.hero.light-mode .accent {
  color: #16A34A;
  text-shadow: none;
}

.hero-desc {
  font-family: "IBM Plex Sans", sans-serif;
  font-size: 1rem;
  line-height: 1.75;
  color: var(--color-muted-fg);
  max-width: 520px;
}

.hero.light-mode .hero-desc { color: #475569; }

/* Social buttons */
.social-row { display: flex; gap: 12px; flex-wrap: wrap; }

.social-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 10px;
  background-color: var(--color-muted);
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
  font-size: 1rem;
  text-decoration: none;
  transition: background-color 0.2s ease, color 0.2s ease, border-color 0.2s ease, transform 0.2s ease;
  cursor: pointer;
}

.social-btn:hover {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border-color: var(--color-accent);
  transform: translateY(-2px);
}

.social-btn:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.hero.light-mode .social-btn {
  background: #FFFFFF;
  border-color: #CBD5E1;
  color: #475569;
}
.hero.light-mode .social-btn:hover {
  background-color: #16A34A;
  color: #FFFFFF;
  border-color: #16A34A;
}

@media (max-width: 768px) {
  .profile-picture { width: 200px; height: 200px; }
  .hero-title { font-size: 2rem; }
}
</style>
