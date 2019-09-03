<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
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
          required
          placeholder="Enter phone number"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="contactMessageGroup" label="Your Message*" label-for="contactMessage">
        <b-form-textarea
          id="contactMessage"
          v-model="form.contactMessage"
          placeholder="Enter here your message..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
      </b-form-group>

      <b-form-group id="contactConsentGroup" label="Some Serious Stuff*" label-for="contactConsent">
        <b-form-checkbox-group v-model="form.contactConsent" id="contactConsent">
          <b-form-checkbox value="yes" required>
            Dude, feel free to use my contact details to respond to my inquiry.
          </b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>

      <b-button type="submit" variant="primary">
        Submit <i class="material-icons md-18">send</i>
      </b-button>
      <b-button type="reset" variant="danger">
        Reset <i class="material-icons md-18">cancel</i>
      </b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
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
      show: true
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      alert(JSON.stringify(this.form))
    },
    onReset (evt) {
      evt.preventDefault()
      // Reset form values
      this.form.contactEmail = ''
      this.form.contactName = ''
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
  .material-icons.md-18 {
    font-size: 18px;
    vertical-align: text-bottom;
  }
</style>
