<template lang="pug">
section.section--contact#contact
  svg.cloud__wrapper#clouds(xmlns="http://www.w3.org/2000/svg" version="1.1" viewBox="0 0 100 100" preserveAspectRatio="none")
    path(d="M-5 100 Q 0 20 5 100 Z M0 100 Q 5 0 10 100 M5 100 Q 10 30 15 100 M10 100 Q 15 10 20 100 M15 100 Q 20 30 25 100 M20 100 Q 25 -10 30 100 M25 100 Q 30 10 35 100 M30 100 Q 35 30 40 100 M35 100 Q 40 10 45 100 M40 100 Q 45 50 50 100 M45 100 Q 50 20 55 100 M50 100 Q 55 40 60 100 M55 100 Q 60 60 65 100 M60 100 Q 65 50 70 100 M65 100 Q 70 20 75 100 M70 100 Q 75 45 80 100 M75 100 Q 80 30 85 100 M80 100 Q 85 20 90 100 M85 100 Q 90 50 95 100 M90 100 Q 95 25 100 100 M95 100 Q 100 15 105 100 Z")
  .section--wrapper.contact-wrapper
    .contact-info
      h1.contact-info__title CONTACT ME
      h2.contact-info__name John DOE, Ad commodo
      .contact-info__icons-wrapper
        a(href="#")
          i.icon.icon-phone.contact-info__icon
        a(href="mailto:helene.andre.06@gmail.com" target="_top")
          i.icon.icon-email.contact-info__icon
        a(href="#" target="_blank")
          i.icon.icon-github.contact-info__icon
        a(href="#" target="_blank")
          i.icon.icon-codepen.contact-info__icon
        a(href="#" target="_blank")
          i.icon.icon-linkedin.contact-info__icon
    form#form.contact-form(action="https://formspree.io/helene.andre.06@gmail.com" @submit="checkForm" method="post")
      .contact-form__field-wrapper
        input#name.contact-form__field(v-model="name" @keyup="validateField()" type="text" name="name" placeholder="Name" autocomplete="off")
        .invalid-field-message This field is required
      .contact-form__field-wrapper
        input#email.contact-form__field(v-model="email" @keyup="validateField()" type="email" name="email" placeholder="Email" autocomplete="off")
        .invalid-field-message This field is required
        .invalid-email-message Must be a valid email
      .contact-form__field-wrapper
        input#subject.contact-form__field(v-model="subject" @keyup="validateField()" type="text" name="subject" placeholder="Subject" autocomplete="off")
        .invalid-field-message This field is required
      .contact-form__field-wrapper
        textarea#message.contact-form__field(v-model="message" @keyup="validateField()" name="message" placeholder="Message" rows="6" cols="80")
        .invalid-field-message This field is required

      .contact-form__send-wrapper
        input#send-button(type="submit" value="Send")
</template>

<script>
export default {
  data: () => ({
    errors: [],
    name: null,
    email: null,
    subject: null,
    message: null
  }),
  methods:{
    checkForm: function (e) {
      if (this.name && this.email && this.subject && this.message) return true

      this.errors = [];

      if (!this.name) document.getElementById('name').parentElement.classList.add('invalid-field')

      if (!this.email) document.getElementById('email').parentElement.classList.add('invalid-field')

      if (!this.subject) document.getElementById('subject').parentElement.classList.add('invalid-field')

      if (!this.message) document.getElementById('message').parentElement.classList.add('invalid-field')

      e.preventDefault();
    },
    validateField: function (e) {
      let field = document.getElementById(event.target.id)
      let fieldWrapper = field.parentElement
      let fieldValue = field.value.trim()

      if (!fieldValue) {
        fieldWrapper.classList.add('invalid-field')
        fieldWrapper.classList.remove('correct-field')
        fieldWrapper.classList.remove('invalid-email')
        return false 
      }

      // If field is email field.
      else if (field.id === 'email' && !/^.+@.+\.[a-zA-Z]{2,}$/.test(fieldValue)) {
        fieldWrapper.classList.remove('invalid-field')
        fieldWrapper.classList.add('invalid-email')
        return false 
      }
      
      else {
        fieldWrapper.classList.remove('invalid-field')
        fieldWrapper.classList.remove('invalid-email')
        fieldWrapper.classList.add('correct-field')
        return true 
      }
    }
  }
}
</script>

<style lang="scss">
/**================ div separation interests /.section--contact ===================**/
.container .cloud__wrapper {display: block;}

.cloud__wrapper {
  width: 100%; 
  min-width: 1200px;
  max-height: 150px;
  left: 0%;
}

#clouds {
  position: absolute;
  bottom: 99%;
  & path {
    fill: #fff;
    stroke: #fff;
  }
}
/**==============================================================================**/

/**=========================== section--contact =================================**/
input[type=submit] {
  border-radius: 0px; 
  -webkit-border-radius:0px;
  appearance: none;
  -webkit-appearance: none;
}

/* Contact section wrapper. */
.section--contact {
  padding-top: 100px;
  height: 70vh; 
}

/* Contact sub-section wrapper. */
.contact-wrapper {
  background-color: #fff;
  height: auto;
  display: flex; 
  justify-content: center;
}

.contact-info {
  height: 34em;
  width: 40%;
  &__title {
    position: relative;
    letter-spacing: 2px;
    top: 0%;
    margin-bottom: 30px;
    text-align: left;
    font-size: 3em;
  }
  &__name {
    font-family: 'Roboto', arial;
    letter-spacing: 1px;
    margin-bottom: 45px;
    font-size: 14px;
  }
  &__icons-wrapper {
    font-size: 36px;
    height: 38px;
    display: flex;
    flex-wrap: wrap; 
    justify-content: left;
    letter-spacing: 17px;
    color: #bdbdbd;
  }
  &__icon {
    transition: 0.3s;
    cursor: pointer; 
    &:hover {color: #2e7d32;}
  }
}

.contact-form {
  height: 34em;
  width: 360px;  
  &__field-wrapper, &__send-wrapper {
    width: 100%;
    margin-bottom: 9%;
    position: relative;
  }
  &__field {
    width: 94%;
    background-color: #f5f5f5;
    outline: none;
    border: none;
    border-bottom: 2px solid transparent;
    transition: 0.3s ease-in-out;
    font-family: 'Roboto', arial;
    font-size: 14px;
    padding: 3%;
    &:focus {border-color: rgba(46, 125, 50, 0.78);}
  }
}

textarea {resize: none;}

input {color: #190e0b;}

.send-button-wrapper {
  position: absolute;
  top: 0%; 
}

#send-button {
  width: 4em;
  position: absolute;
  right: 0%;
  padding: 3px 10px 7px 10px;
  font-size: 14px;
  font-family: 'Roboto', arial;
  color: #2e7d32;
  border: 1px solid #2e7d32;
  background-color: #fff;
  outline: none;
  transition: 0.3s ease-in-out;
  &:hover {
    cursor: pointer;
    opacity: 1;
    color: #757575;
    border-color: #757575;
  } 
}
/**=====================================================================**/
/**=========================  error messages ===========================**/
.invalid-field-message, .invalid-email-message { 
  font-style: italic;
  font-size: 12px; 
  padding-top: 2px; 
  color: #e53935; 
  position: absolute;
  top: 100%;
  margin-top: 3px;
  opacity: 0;
  z-index: -1;
  transition: 0.3s ease-in-out;
}

.invalid-field .invalid-field-message,
.invalid-email .invalid-email-message {
  opacity: 1; 
  z-index: 1;
}

.invalid-field input, 
.invalid-email input, 
.invalid-field textarea,
.invalid-field input:focus, 
.invalid-email input:focus, 
.invalid-field textarea:focus {
  border-color: #e53935;
}

.correct-field input, 
.correct-field textarea,
.correct-field input:focus, 
.correct-field textarea:focus {
  border-color: #81c784;
}
/**=====================================================================**/

/**========================== media queries ============================**/
@media screen and (max-width: 992px) {
  /* Contact section. */
  .section--contact {
    padding-left: 3%; 
    padding-right: 3%; 
  }
}

@media screen and (max-width: 768px){
  .contact-info {
    width: 50%;
    &__icons-wrapper {
      font-size: 32px;
    }
    &__name {
      font-size: 13px; 
    }
  }
}

@media screen and (max-width: 600px) {
  .section--contact {height: 120vh;}

  .contact-wrapper {flex-direction: column;}

  .contact-info {
    width: 70%;
    position: relative;
    left: 50%;
    transform: translateX(-50%);
    text-align: center; 
    height: 200px; 
    &__title {
      font-size: 2.5em;
      text-align: center; 
    }
    &__icons-wrapper {
      justify-content: space-between;
      letter-spacing: unset;
    }
  }

  .contact-form {
    width: 70%;
    position: relative;
    left: 50%;
    transform: translateX(-50%);
    padding-top: 30px;
    &__field-wrapper, 
    &__send-wrapper {
      left: 50%;
      transform: translateX(-50%);
    }
  }

  #send-button {
    right: 50%; 
    transform: translateX(50%);
  } 
}

@media screen and (max-height: 420px) {
  .section--contact {height: 204vh;}
}
</style>
