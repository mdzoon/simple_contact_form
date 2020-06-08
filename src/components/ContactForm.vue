 <template>
  <div id="contactForm" :class="{ 'form-opened shadow': openForm }">
    <button type="button" class="btn btn-info btn-open rounded-top" :class="{ 'shadow': openForm }" @click="openForm=!openForm">Contact Me</button>
    <div class="container border border-left-0 border-info p-3 mb-5 bg-white rounded-right">
      <button type="button" class="close" aria-label="Close" @click="closeContactForm">
        <span aria-hidden="true"><i class="material-icons md-18">cancel</i></span>
      </button>
      <b-form @submit="onSubmit" @reset="onReset">

        <p class="mt-5">Remember: The fields with asteriks are mandatory.</p>

        <b-form-group
          id="contactNameGroup"
          label="Your Name*"
          label-for="contactName"
          :class="{invalid: formSubmitted && $v.form.contactName.$invalid}">
          <b-form-input
            id="contactName"
            v-model="$v.form.contactName.$model"
            placeholder="Enter name"
            aria-describedby=""
          ></b-form-input>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactName.required">
            This field shoud not be empty!
          </p>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactName.minLength">
            Your name must contain at least {{$v.form.contactName.$params.minLength.min}} letters.
          </p>
        </b-form-group>

        <b-form-group
          id="contactEmailGroup"
          label="Email address*"
          label-for="contactEmail"
          :class="{invalid: formSubmitted && $v.form.contactEmail.$invalid}">
          <b-form-input
            id="contactEmail"
            v-model="$v.form.contactEmail.$model"
            type="email"
            placeholder="Enter email"
          ></b-form-input>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactEmail.required">
            This field shoud not be empty!
          </p>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactEmail.email">
            Please provide valid email!
          </p>
        </b-form-group>

        <b-form-group
          id="contactPhoneGroup"
          label="Phone Number"
          label-for="contactPhone"
          :class="{invalid: formSubmitted && $v.form.contactPhone.$invalid}">
          <b-form-input
            id="contactPhone"
            v-model="$v.form.contactPhone.$model"
            type="tel"
            placeholder="Enter phone number"
          ></b-form-input>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactPhone.numeric">
            Please enter only numbers!
          </p>
        </b-form-group>

        <b-form-group
          id="contactMessageGroup"
          label="Your Message*"
          label-for="contactMessage"
          :class="{invalid: formSubmitted && $v.form.contactMessage.$invalid}">
          <b-form-textarea
            id="contactMessage"
            v-model="$v.form.contactMessage.$model"
            placeholder="Enter here your message..."
            rows="3"
            max-rows="6"
          ></b-form-textarea>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactMessage.required">
            This field shoud not be empty!
          </p>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactMessage.minLength">
            Your name must have at least {{$v.form.contactMessage.$params.minLength.min}} characters.
          </p>
        </b-form-group>

        <b-form-group id="contactConsentGroup" label="Some Serious GDPR Stuff*" label-for="contactConsent">
          <b-form-checkbox
            id="contactConsent"
            v-model="$v.form.contactConsent.$model"
            name="consent"
            :class="{invalid: formSubmitted && $v.form.contactConsent.$invalid}"
          >
            Dude, feel free to use my contact details to respond to my inquiry.
          </b-form-checkbox>
          <p class="alert alert-danger mt-1" role="alert" v-if="formSubmitted && !$v.form.contactConsent.$model">
            Please confirm you want us to contact you!
          </p>
        </b-form-group>

        <br>

        <div>
          <div class="row justify-content-around">
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
          <div class="mt-3">
            <p class="alert alert-success" role="alert" v-if="submitStatus === 'OK'">Thank you for your submission!</p>
            <p class="alert alert-danger" role="alert" v-if="submitStatus === 'ERROR'">Please fill in the form correctly.</p>
            <p class="alert alert-info" role="alert" v-if="submitStatus === 'PENDING'">Sending...</p>
          </div>
        </div>

      </b-form>
      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ form }}</pre>
      </b-card>
    </div>
  </div>
</template>

<script>
import { required, minLength, email, numeric } from 'vuelidate/lib/validators'

export default {
  name: 'ContactForm',
  data () {
    return {
      form: {
        contactName: '',
        contactEmail: '',
        contactPhone: '',
        contactMessage: '',
        contactConsent: false
      },
      openForm: false,
      submitStatus: '',
      formSubmitted: false
    }
  },
  methods: {
    // openContactForm() {
    //   this.openForm = true
    // },
    closeContactForm () {
      this.openForm = false
    },
    setContactName (value) {
      this.contactName = value
    },
    onSubmit (evt) {
      evt.preventDefault()
      console.log(this.$v.form.contactName)
      this.$v.form.$touch()
      if (this.$v.form.$invalid || !this.$v.form.contactConsent.$model) {
        this.submitStatus = 'ERROR'
        this.formSubmitted = true
      } else {
        // do your submit logic here
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
          alert(JSON.stringify(this.form))
        }, 500)
      }
    },
    onReset (evt) {
      evt.preventDefault()
      // Reset form values
      this.form.contactName = ''
      this.form.contactEmail = ''
      this.form.contactPhone = ''
      this.form.contactMessage = ''
      this.form.contactConsent = false
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  },
  validations: {
    form: {
      contactName: {
        required,
        minLength: minLength(3)
      },
      contactEmail: {
        required,
        email
      },
      contactPhone: {
        numeric
      },
      contactMessage: {
        required,
        minLength: minLength(5)
      },
      contactConsent: {
        required
      }
    }
  }
}
</script>

<style scoped lang="scss">
  $color-info: #17a2b8;
  $invalid-input: #721c24;
  $form-width: 80vw;
  $size-adjustment: 30vw;

  .material-icons.md-18 {
    font-size: 18px;
    vertical-align: text-bottom;
  }
  #contactForm {
    position: fixed;
    top: 2vh;
    left: -$form-width;
    width: $form-width;
    height: 96vh;
    transition: 1.5s left ease-out;
    .container {
      height: 100%;
      overflow-y: scroll;
    }
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
      left: -$form-width + $size-adjustment;
      width: $form-width - $size-adjustment;
    }
  }
  .alert {
    font-size: .75rem;
    padding: .375rem .75rem;
  }
  .invalid input, .invalid textarea {
    border: 1px solid $invalid-input;
    background-color: adjust-color($invalid-input, $lightness: 65%);
  }

</style>
