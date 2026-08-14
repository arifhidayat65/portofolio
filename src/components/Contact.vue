<template>
  <div class="section contact-section" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="section-header text-center mb-5" data-aos="fade-down" data-aos-duration="700">
        <span class="section-label mono">// contact</span>
        <h2 class="section-title">Get In Touch</h2>
        <div class="title-line"></div>
        <p class="section-sub mt-3">Have a project in mind? Let's talk.</p>
      </div>
      <div class="row justify-content-center">
        <div class="col-md-7" data-aos="fade-up" data-aos-duration="700">
          <form @submit.prevent="sendEmail" class="contact-form" novalidate>
            <div class="mb-4">
              <label for="name" class="form-label">Name</label>
              <input type="text" class="form-control" id="name" v-model="name" required autocomplete="name" placeholder="Your name">
            </div>
            <div class="mb-4">
              <label for="email" class="form-label">Email</label>
              <input type="email" class="form-control" id="email" v-model="email" required autocomplete="email" placeholder="your@email.com">
            </div>
            <div class="mb-4">
              <label for="message" class="form-label">Message</label>
              <textarea class="form-control" id="message" rows="5" v-model="text" required placeholder="Tell me about your project..."></textarea>
            </div>
            <div class="text-center">
              <button type="submit" class="submit-btn">Send Message</button>
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
  components: { Snackbar },
  props: {
    nightMode: { type: Boolean },
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
        setTimeout(() => { this.showSnackbar = val; }, 1000);
      }
    },
    sendEmail() {
      if (!this.email || !this.name || !this.text) {
        this.showSnackbar = true;
        this.snackbarMessage = "Please fill all the fields";
        this.snackbarColor = "#F59E0B";
      } else {
        emailjs
          .send(
            config.emailjs.serviceID,
            config.emailjs.templateID,
            { user_email: this.email, from_name: this.name, message_html: this.text, to_name: "Arif Hidayat" },
            config.emailjs.userID
          )
          .then(() => {
            this.showSnackbar = true;
            this.snackbarMessage = "Message sent successfully!";
            this.snackbarColor = "#22C55E";
            this.name = "";
            this.email = "";
            this.text = "";
          })
          .catch(() => {
            this.showSnackbar = true;
            this.snackbarMessage = "Oops! Something went wrong.";
            this.snackbarColor = "#EF4444";
          });
      }
    },
  },
};
</script>

<style scoped>
.section {
  background-color: var(--color-primary);
  padding: 80px 0;
}
.section.light-mode { background-color: #F1F5F9; }

.section-label {
  font-size: 0.8rem;
  color: var(--color-accent);
  display: block;
  margin-bottom: 8px;
  letter-spacing: 0.06em;
}
.section.light-mode .section-label { color: #16A34A; }

.section-title {
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  font-weight: 700;
  color: var(--color-foreground);
  margin-bottom: 12px;
}
.section.light-mode .section-title { color: #0F172A; }

.section-sub {
  color: var(--color-muted-fg);
  font-size: 0.95rem;
}
.section.light-mode .section-sub { color: #64748B; }

.title-line {
  width: 48px;
  height: 3px;
  background: var(--color-accent);
  border-radius: 2px;
  margin: 0 auto;
  box-shadow: 0 0 8px rgba(34, 197, 94, 0.4);
}
.section.light-mode .title-line { box-shadow: none; }

/* Form */
.contact-form { background: var(--color-card); border: 1px solid var(--color-border); border-radius: var(--border-radius); padding: 40px; }
.section.light-mode .contact-form { background: #FFFFFF; border-color: #E2E8F0; }

.form-label {
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 500;
  font-size: 0.85rem;
  color: var(--color-muted-fg);
  margin-bottom: 6px;
  display: block;
}
.section.light-mode .form-label { color: #475569; }

.form-control {
  background-color: var(--color-muted);
  border: 1px solid var(--color-border);
  color: var(--color-foreground);
  border-radius: 8px;
  font-family: "IBM Plex Sans", sans-serif;
  font-size: 0.95rem;
  padding: 10px 14px;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
  width: 100%;
}

.form-control::placeholder { color: var(--color-border); }

.form-control:focus {
  outline: none;
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px rgba(34, 197, 94, 0.15);
  background-color: var(--color-muted);
  color: var(--color-foreground);
}

.section.light-mode .form-control {
  background-color: #F8FAFC;
  border-color: #CBD5E1;
  color: #0F172A;
}
.section.light-mode .form-control::placeholder { color: #94A3B8; }
.section.light-mode .form-control:focus {
  border-color: #16A34A;
  box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.12);
  background-color: #FFFFFF;
}

.submit-btn {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border: none;
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 600;
  font-size: 0.95rem;
  padding: 12px 36px;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.2s ease, box-shadow 0.2s ease;
  outline: none;
}

.submit-btn:hover {
  background-color: #16A34A;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(34, 197, 94, 0.3);
}

.submit-btn:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.section.light-mode .submit-btn { background-color: #16A34A; }
.section.light-mode .submit-btn:hover { background-color: #15803D; box-shadow: 0 6px 16px rgba(22, 163, 74, 0.25); }
</style>
