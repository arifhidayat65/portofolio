<template>
  <div :class="{ 'bg-white': !nightMode, 'bg-dark': nightMode }" class="d-flex align-items-center min-vh-100">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-md-6 text-center mb-4 mb-md-0">
          <img :src="picture" class="profile-picture" alt="Profile Picture" data-aos="fade-up" data-aos-duration="1000">
        </div>
        <div class="col-md-6">
          <div data-aos="fade-down" data-aos-duration="1000">
            <h1 class="display-4 fw-bold" :class="{ 'text-dark': !nightMode, 'text-light': nightMode }">Welcome!</h1>
            <p class="lead" v-html="description"></p>
            <div class="d-flex justify-content-center justify-content-md-start mt-4">
              <a :href="linkedin" target="_blank" class="btn btn-outline-primary me-3" v-tooltip.bottom="'LinkedIn'">
                <i class="fab fa-linkedin"></i>
              </a>
              <a :href="github" target="_blank" class="btn btn-outline-primary me-3" v-tooltip.bottom="'GitHub'">
                <i class="fab fa-github"></i>
              </a>
              <a :href="twitter" target="_blank" class="btn btn-outline-primary me-3" v-tooltip.bottom="'Twitter'">
                <i class="fab fa-twitter"></i>
              </a>
              <a :href="facebook" target="_blank" class="btn btn-outline-primary" v-tooltip.bottom="'Facebook'">
                <i class="fab fa-facebook"></i>
              </a>
            </div>
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
    nightMode: {
      type: Boolean,
    },
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
.min-vh-100 {
  min-height: 100vh;
}

.profile-picture {
  width: 250px;
  height: 250px;
  object-fit: cover;
  border-radius: 50%;
  border: 5px solid var(--primary-color);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.btn-outline-primary {
  color: var(--primary-color);
  border-color: var(--primary-color);
  border-width: 2px;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  transition: all 0.3s ease;
}

.btn-outline-primary:hover {
  background-color: var(--primary-color);
  color: var(--surface-color);
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

.lead {
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  line-height: 1.7;
}

@media (max-width: 768px) {
  .display-4 {
    font-size: 2.5rem;
  }
  .profile-picture {
    width: 200px;
    height: 200px;
  }
}
</style>