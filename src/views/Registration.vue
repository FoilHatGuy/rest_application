<template>
  <div class="registration">
    <div class="form">
      <div id="label">Регистрация</div>
      <input id="login" placeholder="Login">
      <input id="password" type="password" placeholder="Password">
      <input id="password_repeat" type="password" placeholder="Repeat password">
      <input id="email" type="email" placeholder="Email">
      <button type="submit" id="button" @click="sendData">Зарегестрироваться</button>
    </div>
  </div>
</template>

<script>
import emailjs from '@emailjs/browser';

export default {
  data() {
    return {
      sendEmails: false
    }
  },
  name: "Registration",
  methods: {
    sendData() {
      // https://dashboard.emailjs.com/admin
      if (this.sendEmails) {
        emailjs.send('service_v10hdb8', 'template_2lgjdlf', {
          from_name: "Vue app",
          to_name: document.getElementById("login").value,
          message: "Your account was registered successfully in Vue App.",
          link: "some_link.com",
          email: document.getElementById("email").value
        }, 'XcDbXwQoBpQ4eQwzu')
            .then((result) => {
              console.log('SUCCESS!', result.text);
              if (result.text === "OK") this.$router.push('/');
            }, (error) => {
              console.log('FAILED...', error.text);
            });
      }
    }
  }
}
</script>

<style scoped>
.registration {
  margin-top: 50px;
  font-size: 24px;
  padding: 20px;

  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.form {
  width: max-content;
  border-radius: 30px;
  padding: 20px;
  background: var(--color-gray);

  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
#label, #login, #password, #button, #email, #password_repeat{
  margin: 10px 20px;
  font-size: 24px;
}
</style>