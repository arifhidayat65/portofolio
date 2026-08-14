<template>
  <div class="logo-div">
    <span class="logo-name mono">{{ name }}</span><span class="logo-dot">.</span>
  </div>
</template>

<script>
import info from "../../../info";

export default {
  name: "Logo",
  props: {
    nightMode: { type: Boolean },
  },
  data() {
    return {
      name: info.logo_name,
    };
  },
};
</script>

<style scoped>
.logo-div {
  display: inline-flex;
  align-items: baseline;
  gap: 1px;
  text-decoration: none;
}

.logo-name {
  font-size: 1.1rem;
  font-weight: 600;
  letter-spacing: 0.02em;
  color: var(--color-foreground);
  transition: letter-spacing 0.3s ease;
}

.logo-div:hover .logo-name {
  letter-spacing: 0.06em;
}

.logo-dot {
  font-size: 1.3rem;
  font-weight: 700;
  color: var(--color-accent);
}
</style>
