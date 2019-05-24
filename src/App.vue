<template>
  <!-- Material form contact -->
   <mdb-container>
    <mdb-row>
      <mdb-col class="col-lg-6 col-md-8 col-sm-12 mx-auto"></mdb-col>
      <form @submit.prevent="handleSubmit" name="contact" method="POST" netlify-honeypot="bot-field" data-netlify="true" class="w-100">
        <p style="display:none;" class="hidden">
        <label>Don’t fill this out if you're human: <input name="bot-field" /></label>
        </p>
        <p class="h4 text-center mb-4">Write to us</p>
        <div class="grey-text">
          <mdb-input v-model="form.name" name="name" label="Your name" icon="user" group type="text" validate error="wrong" success="right"/>
          <mdb-input v-model="form.email" name="email" label="Your email" icon="envelope" group type="email" validate error="wrong" success="right"/>
          <mdb-input v-model="form.subject" name="subject" label="Subject" icon="tag" group type="text" validate error="wrong" success="right"/>
          <mdb-textarea v-model="form.message" name="message" :rows="2" label="Your message" icon="pencil"/>
        </div>
        <div class="text-center">
          <mdb-btn outline="secondary">Send <mdb-icon far icon="paper-plane" class="ml-1"/></mdb-btn>
        </div>
      </form>
    </mdb-row>
  </mdb-container>
  
</template> 
<script>
  import { 
    mdbInput, 
    mdbBtn, 
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbTextarea,
    mdbIcon } from 'mdbvue';
  export default {
    name: 'Basic',
    data: () => ({
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
    }),
    components: {
      mdbInput,
      mdbBtn,
      mdbContainer,
      mdbRow,
      mdbCol,
      mdbTextarea, 
      mdbIcon
    },
    methods: {
      encode(data) {
        return Object.keys(data)
        .map(key => '${encodeURIComponent(key)}=${encodeURIComponent(data[key])}')
        .join('&')
      },
      handleSubmit() {
        fetch('/', {
          method: 'post',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          },
          body: this.encode({
            'form-name': 'contact',
            ...this.form
          })
        })
        .then(() => console.log('successfully sent'))
        .catch(e => console.error(e))
      }
    }
  }
</script>