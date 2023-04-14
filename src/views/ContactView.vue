<template>
  <div class="contact-page">
    <h1>Send Me a Message</h1>
    <div class="flex-cont">
      <div class="img-cont">
        <img src="@/assets/city_of_belgrade.jpg" alt="city of belgrade photo" />
      </div>
      <div class="form-cont">
        <form class="form" ref="form" @submit.prevent="sendEmail">
          <label class="visibility: hidden" for="name">Name</label>
          <input
            type="text"
            v-model="name"
            name="name"
            placeholder="Your Name"
            id="name"
          />
          <label class="visibility: hidden" for="email">Email</label>
          <input
            type="email"
            v-model="email"
            name="email"
            placeholder="Your Email"
            id="email"
          />
          <label class="visibility: hidden" for="message">Message</label>
          <textarea
            name="message"
            v-model="message"
            cols="30"
            rows="5"
            placeholder="Message"
            id="message"
          >
          </textarea>

          <input type="submit" value="Send" />
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// npm install emailjs-com
import emailjs from "emailjs-com";

export default {
  name: "ContactView",

  data() {
    return {
      name: "",
      email: "",
      message: "",
    };
  },
  methods: {
    sendEmail(e) {
      try {
        emailjs.sendForm(
          "service_veysv5r",
          "template_69el6bn",
          e.target,
          "iAlfj5v_z-TUpuVUG",
          {
            name: this.name,
            email: this.email,
            message: this.message,
          }
        );
      } catch (error) {
        console.log({ error });
      }
      // Reset form field
      this.name = "";
      this.email = "";
      this.message = "";
    },
  },
};
</script>

<style>
.contact-page {
  background-image: url("@/assets/contact_back.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-color: #1f152e;
}

.contact-page {
  height: 100vh;
  padding: 64px 10px;
}

.flex-cont {
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 5px;
}

label {
  float: left;
  color: #fff;
  font-size: 1.5em;
}

input[type="text"],
[type="email"],
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 4px;
  margin-bottom: 16px;
  resize: vertical;
}

input[type="submit"] {
  width: 100%;
  background-color: #f2f;
  color: #000;
  padding: 10px 20px;
  border: 3px solid #f2f;
  border-radius: 4px;
  cursor: pointer;
}

input[type="submit"]:hover {
  border: 3px solid #fff;
}

@media (max-width: 1700px) {
  .contact-page {
    flex-direction: column;
    gap: unset;
    height: auto;
    padding: 80px 10px;
  }

  .flex-cont {
    flex-direction: column;
    gap: unset;
  }

  .form-cont {
    margin-top: 60px;
    max-width: 800px;
  }
}

@media (max-width: 767px) {
  .contact-page h1 {
    font-size: 1.5em;
  }
}
</style>
