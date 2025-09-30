<template>
  <div class="py-5" :class="{ 'bg-light': !nightMode, 'bg-dark': nightMode }">
    <div class="container">
      <div class="text-center mb-5" data-aos="fade-down" data-aos-duration="1000">
        <h2 class="display-5 fw-bold">Contact</h2>
        <div class="title-divider"></div>
      </div>
      <div class="row justify-content-center">
        <div class="col-md-8">
          <form @submit.prevent="sendEmail">
            <div class="mb-3">
              <label for="name" class="form-label">Name</label>
              <input type="text" class="form-control" id="name" v-model="name" required>
            </div>
            <div class="mb-3">
              <label for="email" class="form-label">Email</label>
              <input type="email" class="form-control" id="email" v-model="email" required>
            </div>
            <div class="mb-3">
              <label for="message" class="form-label">Message</label>
              <textarea class="form-control" id="message" rows="5" v-model="text" required></textarea>
            </div>
            <div class="text-center">
              <button type="submit" class="btn btn-primary">Send Message</button>
            </div>
          </form>
        </div>
      </div>
    </div>
    <Snackbar :showSnackbar="showSnackbar" @close="closeSnackbar" :snackbarMessage="snackbarMessage" :snackbarColor="snackbarColor" />
  </div>
</template>

<script>
import config from "../../config";
import emailjs from "emailjs-com";
import Snackbar from "./helpers/Snackbar.vue";

export default {
  name: "Contact",
  components: {
    Snackbar,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      name: "",
      email: "",
      text: "",
      showSnackbar: false,
      snackbarMessage: "",
      snackbarColor: "",
    };
  },
  methods: {
    closeSnackbar(val) {
      if (!val) {
        setTimeout(() => {
          this.showSnackbar = val;
        }, 1000);
      }
    },
    sendEmail() {
      if (!this.email || !this.name || !this.text) {
        this.showSnackbar = true;
        this.snackbarMessage = "Please fill all the fields";
        this.snackbarColor = "rgb(212, 149, 97)"; // This should be updated to a new color
      } else {
        var obj = {
          user_email: this.email,
          from_name: this.name,
          message_html: this.text,
          to_name: "Ronyell Henrique", // This should be changed to the user's name
        };

        emailjs
          .send(
            config.emailjs.serviceID,
            config.emailjs.templateID,
            obj,
            config.emailjs.userID
          )
          .then(
            (result) => {
              this.showSnackbar = true;
              this.snackbarMessage = "Thanks! Message received.";
              this.snackbarColor = "var(--secondary-color)";
              this.name = "";
              this.email = "";
              this.text = "";
            },
            (error) => {
              this.showSnackbar = true;
              this.snackbarMessage = "Oops! Something went wrong.";
              this.snackbarColor = "#dc3545"; // Bootstrap's danger color
            }
          );
      }
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

.form-control {
    background-color: var(--surface-color);
    color: var(--text-color);
    border: 1px solid #ced4da;
}

.night-mode .form-control {
    background-color: #3a3a3a;
    color: var(--text-color);
    border-color: #6c757d;
}

.form-control:focus {
    background-color: var(--surface-color);
    color: var(--text-color);
    border-color: var(--primary-color);
    box-shadow: 0 0 0 0.25rem rgba(var(--bs-primary-rgb), 0.25);
}

.night-mode .form-control:focus {
    background-color: #3a3a3a;
    color: var(--text-color);
}

.btn-primary {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
    color: var(--surface-color);
    padding: 12px 30px;
    font-weight: bold;
}
</style>