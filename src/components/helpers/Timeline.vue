<template>
  <div>
    <h3 class="text-center mb-4">{{ data.title }}</h3>
    <ul class="timeline">
      <li v-for="(item, index) in data.data" :key="index" class="timeline-item" data-aos="fade-up" :data-aos-delay="index * 100">
        <div class="timeline-marker"></div>
        <div class="timeline-content">
          <h4 class="h5">{{ item.name }}, {{ item.place }}</h4>
          <h5 class="h6">{{ item.degree || item.position }} {{ item.gpa ? `(${item.gpa})` : '' }}</h5>
          <div class="text-muted small">{{ item.date }}</div>
          <p class="mt-2">{{ item.description }}</p>
          <div>
            <span v-for="skill in item.skills" :key="skill" class="badge me-2 mb-2">{{ skill }}</span>
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
    data: {
      type: Object,
    },
    nightMode: {
      type: Boolean,
    },
  },
};
</script>

<style scoped>
.timeline {
  list-style: none;
  padding: 0;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  top: 0;
  left: 10px;
  height: 100%;
  width: 2px;
  background: var(--surface-color);
}

.timeline-item {
  position: relative;
  padding-left: 40px;
  margin-bottom: 30px;
}

.timeline-marker {
  position: absolute;
  top: 5px;
  left: 0;
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background-color: var(--surface-color);
  border: 3px solid var(--primary-color);
  transition: transform 0.3s;
}

.timeline-item:hover .timeline-marker {
  transform: scale(1.2);
}

.timeline-content {
  background-color: var(--surface-color);
  padding: 20px;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  transition: box-shadow 0.3s;
}

.timeline-content:hover {
    box-shadow: 0 15px 25px rgba(0,0,0,0.15);
}

.badge {
  background-color: var(--primary-color);
  color: var(--surface-color);
  font-weight: 500;
}

.night-mode .badge {
    background-color: var(--secondary-color);
    color: #000;
}
</style>