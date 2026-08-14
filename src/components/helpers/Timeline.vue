<template>
  <div>
    <h3 class="timeline-heading text-center mb-4">{{ data.title }}</h3>
    <ul class="timeline">
      <li
        v-for="(item, index) in data.data"
        :key="index"
        class="timeline-item"
        data-aos="fade-up"
        :data-aos-delay="index * 100"
      >
        <div class="timeline-marker"></div>
        <div class="timeline-content">
          <h4 class="tc-name">{{ item.name }}</h4>
          <div class="tc-place">{{ item.place }}</div>
          <div class="tc-role mono">{{ item.degree || item.position }}</div>
          <div class="tc-date">{{ item.date }}</div>
          <p class="tc-desc" v-if="item.description">{{ item.description }}</p>
          <div class="tc-tags" v-if="item.skills && item.skills.length">
            <span class="tc-tag mono" v-for="skill in item.skills" :key="skill">{{ skill }}</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Timeline",
  props: {
    data: { type: Object },
    nightMode: { type: Boolean },
  },
};
</script>

<style scoped>
.timeline-heading {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--color-accent);
  letter-spacing: 0.04em;
  text-transform: uppercase;
  font-family: "IBM Plex Sans", sans-serif;
}

.timeline {
  list-style: none;
  padding: 0;
  margin: 0;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  top: 8px;
  left: 10px;
  bottom: 0;
  width: 1px;
  background: linear-gradient(to bottom, var(--color-accent), transparent);
  opacity: 0.4;
}

.timeline-item {
  position: relative;
  padding-left: 40px;
  margin-bottom: 28px;
}

.timeline-marker {
  position: absolute;
  top: 6px;
  left: 4px;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background-color: var(--color-background);
  border: 2px solid var(--color-accent);
  box-shadow: 0 0 6px rgba(34, 197, 94, 0.4);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  z-index: 1;
}

.timeline-item:hover .timeline-marker {
  transform: scale(1.3);
  box-shadow: 0 0 12px rgba(34, 197, 94, 0.6);
}

.timeline-content {
  background-color: var(--color-card);
  border: 1px solid var(--color-border);
  padding: 18px 20px;
  border-radius: 10px;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
}

.timeline-item:hover .timeline-content {
  border-color: rgba(34, 197, 94, 0.4);
  box-shadow: 0 4px 20px rgba(0,0,0,0.3);
}

.tc-name {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--color-foreground);
  margin-bottom: 2px;
}

.tc-place {
  font-size: 0.8rem;
  color: var(--color-muted-fg);
  margin-bottom: 4px;
}

.tc-role {
  font-size: 0.8rem;
  color: var(--color-accent);
  margin-bottom: 2px;
}

.tc-date {
  font-size: 0.75rem;
  color: var(--color-border);
  margin-bottom: 8px;
}

.tc-desc {
  font-size: 0.85rem;
  color: var(--color-muted-fg);
  line-height: 1.6;
  margin-bottom: 10px;
}

.tc-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.tc-tag {
  font-size: 0.7rem;
  background-color: var(--color-muted);
  color: var(--color-muted-fg);
  border: 1px solid var(--color-border);
  padding: 2px 7px;
  border-radius: 4px;
  white-space: nowrap;
}
</style>
