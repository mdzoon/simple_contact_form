<template>
  <div id="contactForm" :class="{ 'form-opened shadow': openForm }">
    <button type="button" class="btn btn-info btn-open rounded-top" :class="{ 'shadow': openForm }" @click="openForm=!openForm">Contact Me</button>
    <div class="container border border-left-0 border-info p-3 mb-5 bg-white rounded-right">
      <button type="button" class="close" aria-label="Close" @click="closeContactForm">
        <span aria-hidden="true"><i class="material-icons md-18">cancel</i></span>
      </button>
      <b-form @submit="onSubmit" @reset="onReset">
        <br>
        <p>Remember: The fields with asteriks are mandatory.</p>
        <b-form-group id="contactNameGroup" label="Your Name*" label-for="contactName">
          <b-form-input
            id="contactName"
            v-model="form.contactName"
            required
            placeholder="Enter name"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="contactEmailGroup" label="Email address*" label-for="contactEmail">
          <b-form-input
            id="contactEmail"
            v-model="form.contactEmail"
            type="email"
            required
            placeholder="Enter email"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="contactPhoneGroup" label="Phone Number" label-for="contactPhone">
          <b-form-input
            id="contactPhone"
            v-model="form.contactPhone"
            type="tel"
            placeholder="Enter phone number"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="contactMessageGroup" label="Your Message*" label-for="contactMessage">
          <b-form-textarea
            id="contactMessage"
            v-model="form.contactMessage"
            required
            placeholder="Enter here your message..."
            rows="3"
            max-rows="6"
          ></b-form-textarea>
        </b-form-group>

        <b-form-group id="contactConsentGroup" label="Some Serious GDPR Stuff*" label-for="contactConsent">
          <b-form-checkbox
            id="contactConsent"
            v-model="form.contactConsent" 
            value="yes"
            required
          >
            Dude, feel free to use my contact details to respond to my inquiry.
          </b-form-checkbox>
        </b-form-group>
        
        <br>

        <div class="row d-flex justify-content-around">
          <b-button type="submit" variant="primary">
            Submit <span aria-hidden="true"><i class="material-icons md-18">arrow_forward</i></span>
          </b-button>
          <b-button type="reset" variant="danger">
            Reset <span aria-hidden="true"><i class="material-icons md-18">close</i></span>
          </b-button>
          <b-button type="button" class="btn btn-info" aria-label="Close" @click="closeContactForm">
            Close <span aria-hidden="true"><i class="material-icons md-18">cancel</i></span>
          </b-button>
        </div>

      </b-form>
      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ form }}</pre>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactForm',
  data () {
    return {
      form: {
        contactName: '',
        contactEmail: '',
        contactPhone: '',
        contactMessage: '',
        contactConsent: []
      },
      openForm: false
    }
  },
  methods: {
    // openContactForm() {
    //   this.openForm = true
    // },
    closeContactForm() {
      this.openForm = false
    },
    onSubmit (evt) {
      evt.preventDefault()
      alert(JSON.stringify(this.form))
    },
    onReset (evt) {
      evt.preventDefault()
      // Reset form values
      this.form.contactName = ''
      this.form.contactEmail = ''
      this.form.contactPhone = ''
      this.form.contactMessage = ''
      this.form.contactConsent = []
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
}
</script>

<style scoped lang="scss">
  $main-color: #17a2b8;
  $form-width: 30vw;

  .material-icons.md-18 {
    font-size: 18px;
    vertical-align: text-bottom;
  }
  #contactForm {
    position: fixed;
    top: 5vh;
    left: -80vw;
    width: 80vw;
    transition: 1.5s all;
    .btn-open {
      position: absolute;
      z-index: -1;
      top: 20rem;
      right: -2.15rem;
      transform: rotate(-90deg) scale(-1) translate(-100%, -100%);
      border-radius: unset;
      &:hover, &:focus {
        -webkit-box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
        box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
      }
    } 
  }
  #contactForm.form-opened {
    left: 0;
  }

  @media (max-width: 767px) {
  .d-flex {
      flex-direction: column;
      align-content: center;
      min-height: 10rem;
    }
  }

  @media (min-width: 768px) {
    #contactForm {
      left: -80vw + $form-width;
      width: 80vw - $form-width;
    }
  }
</style>
