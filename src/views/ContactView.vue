<template>
  <div class="contact-page h-screen px-16 pt-16">
    <div class="img-cont">
      <img src="@/assets/city_of_belgrade.jpg" alt="city of belgrade photo" />
    </div>
    <div class="form-cont">
      <form class="form" ref="form" @submit.prevent="sendEmail">
        <label>Name</label>
        <input type="text" v-model="name" name="name" placeholder="Your Name" />
        <label>Email</label>
        <input
          type="email"
          v-model="email"
          name="email"
          placeholder="Your Email"
        />
        <label>Message</label>
        <textarea
          name="message"
          v-model="message"
          cols="30"
          rows="5"
          placeholder="Message"
        >
        </textarea>

        <input type="submit" value="Send" />
      </form>
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
.contact-page::before {
  content: "";
  position: fixed;
  left: 0;
  right: 0;
  z-index: -1;
  display: block;
  background-image: url("@/assets/contact_back.jpg");
  width: 100%;
  height: 100%;
  background-repeat: no-repeat;
  background-size: cover;
}

.contact-page {
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 5px;
}

label {
  float: left;
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
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type="submit"]:hover {
  background-color: #888;
  color: #fff;
}

@media (max-width: 1800px) {
  .contact-page {
    flex-direction: column;
  }

  .form-cont {
    max-width: 800px;
  }
}
</style>
