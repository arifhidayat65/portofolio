<template>
  <div class="py-5" :class="{ 'bg-light': !nightMode, 'bg-dark': nightMode }">
    <div class="container">
      <div class="text-center mb-5" data-aos="fade-down" data-aos-duration="1000">
        <h2 class="display-5 fw-bold">Portfolio</h2>
        <div class="title-divider"></div>
      </div>

      <ul class="nav nav-pills justify-content-center mb-4">
        <li class="nav-item">
          <a class="nav-link" :class="{ active: activeTab === 'development' }" @click="activeTab = 'development'">Development</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" :class="{ active: activeTab === 'design' }" @click="activeTab = 'design'">Design</a>
        </li>
      </ul>

      <div v-if="activeTab === 'development'">
        <div class="row g-4">
          <div class="col-lg-4 col-md-6" v-for="(portfolio, index) in displayedPortfolios" :key="index" data-aos="fade-up" :data-aos-delay="index * 100">
            <Card :portfolio="portfolio" :nightMode="nightMode" @show="showModalFn" />
          </div>
        </div>
        <div class="text-center mt-4" v-if="all_info.length > displayedPortfolios.length">
          <button class="btn btn-primary" @click="loadMore">Load More</button>
        </div>
      </div>

      <div v-if="activeTab === 'design'">
          <div class="row g-4">
            <div class="col-lg-4 col-md-6" v-for="(design, index) in design_info" :key="index" data-aos="fade-up" :data-aos-delay="index * 100">
                <Card :portfolio="design" :nightMode="nightMode" @show="showDesignModalFn" />
            </div>
        </div>
      </div>

    </div>

    <Modal v-if="showModal" :portfolio="modal_info" :nightMode="nightMode" @close="closeModal" />
    <DesignModal v-if="showDesignModal" :portfolio="design_modal_info" :nightMode="nightMode" @close="closeModal" />
  </div>
</template>

<script>
import Card from "./helpers/Card.vue";
import Modal from "./helpers/Modal.vue";
import DesignModal from "./helpers/DesignModal.vue";
import info from "../../info";

export default {
  name: "Portfolio",
  components: {
    Card,
    Modal,
    DesignModal,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      activeTab: 'development',
      all_info: info.portfolio,
      design_info: info.portfolio_design,
      displayedPortfolios: [],
      showModal: false,
      showDesignModal: false,
      modal_info: {},
      design_modal_info: {},
      itemsPerLoad: 6,
    };
  },
  created() {
    this.loadMore();
  },
  methods: {
    loadMore() {
      const currentLength = this.displayedPortfolios.length;
      const newItems = this.all_info.slice(currentLength, currentLength + this.itemsPerLoad);
      this.displayedPortfolios.push(...newItems);
    },
    showModalFn(portfolio) {
      this.modal_info = portfolio;
      this.showModal = true;
    },
    showDesignModalFn(design_portfolio) {
      this.design_modal_info = design_portfolio;
      this.showDesignModal = true;
    },
    closeModal() {
      this.showModal = false;
      this.showDesignModal = false;
    },
  },
};
</script>

<style scoped>
.title-divider {
  width: 100px;
  height: 4px;
  background-color: var(--primary-color);
  margin: 1rem auto;
  border-radius: 2px;
}

.nav-pills .nav-link {
  color: var(--text-color);
  cursor: pointer;
}

.nav-pills .nav-link.active {
  background-color: var(--primary-color);
  color: var(--surface-color);
}
</style>