<template>
  <footer class="footer" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-md-6 text-center text-md-start mb-3 mb-md-0">
          <span class="mono copyright">© {{ new Date().getFullYear() }} Arif Hidayat</span>
        </div>
        <div class="col-md-6 text-center text-md-end">
          <a :href="linkedin" target="_blank" rel="noopener" class="social-icon me-3" aria-label="LinkedIn" v-tooltip.top="'LinkedIn'">
            <i class="fab fa-linkedin-in"></i>
          </a>
          <a :href="github" target="_blank" rel="noopener" class="social-icon me-3" aria-label="GitHub" v-tooltip.top="'GitHub'">
            <i class="fab fa-github"></i>
          </a>
          <a :href="twitter" target="_blank" rel="noopener" class="social-icon me-3" aria-label="Twitter" v-tooltip.top="'Twitter'">
            <i class="fab fa-twitter"></i>
          </a>
          <a :href="facebook" target="_blank" rel="noopener" class="social-icon" aria-label="Facebook" v-tooltip.top="'Facebook'">
            <i class="fab fa-facebook-f"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import info from "../../info";

export default {
  name: "Footer",
  props: { nightMode: Boolean },
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
  background-color: var(--color-primary);
  border-top: 1px solid var(--color-border);
  padding: 28px 0;
  color: var(--color-muted-fg);
}

.footer.light-mode {
  background-color: #F1F5F9;
  border-top-color: #E2E8F0;
  color: #64748B;
}

.copyright {
  font-size: 0.85rem;
  color: var(--color-muted-fg);
}

.social-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background-color: var(--color-muted);
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
  font-size: 0.9rem;
  text-decoration: none;
  transition: background-color 0.2s ease, color 0.2s ease, border-color 0.2s ease, transform 0.2s ease;
  cursor: pointer;
}

.social-icon:hover {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border-color: var(--color-accent);
  transform: translateY(-2px);
}

.social-icon:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.footer.light-mode .social-icon {
  background: #FFFFFF;
  border-color: #CBD5E1;
  color: #475569;
}
.footer.light-mode .social-icon:hover {
  background-color: #16A34A;
  color: #FFFFFF;
  border-color: #16A34A;
}
</style>
