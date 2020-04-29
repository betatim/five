<template>
  <main>
    <div class="zeugs">
      <coming-soon />
      <small
        >Wir arbeiten gemeinsam mit Swisscom Trust Services an einer Lösung für
        die QES-Identifikation. Die Plattform für Video-Identifikation,
        videoident.me, wird in den nächsten Tagen zur Verfügung stehen. Sobald
        der Service genutzt werden kann, informieren wir über unseren
        Newsletter. <br /><br />Bestehende Skribble-Nutzer werden wir zusätzlich
        per E-Mail informieren.</small
      >
    </div>
    <div v-show="status === 'start'">
      <h2 class="mt-12 mb-6">Skribble Newsletter</h2>
      <v-form ref="form" v-model="validForm" :lazy-validation="lazy">
        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="E-Mail"
          autocomplete="email"
          required
          outlined
        ></v-text-field>
        <v-btn
          @click="signUp"
          :disabled="!validForm || submitted"
          class="intro__cta mt-md-6"
          large
          color="primary"
          :block="$vuetify.breakpoint.xsOnly"
          >Abonnieren</v-btn
        >
      </v-form>
    </div>
    <div v-show="status === 'subscribed'">
      Sie werden von uns hören!
    </div>
  </main>
</template>

<script>
import ComingSoon from '~/components/ComingSoon.vue'

export default {
  components: {
    ComingSoon,
  },
  data() {
    return {
      status: 'start',
      validForm: true,
      submitted: false,
      email: '',
      emailRules: [
        v => !!v || 'E-Mail benötigt',
        v => /.+@.+\..+/.test(v) || 'E-Mail ungültig',
      ],
      lazy: false,
    }
  },
  methods: {
    signUp() {
      this.submitted = true
      this.$axios
        .$post(
          'https://api.hsforms.com/submissions/v3/integration/submit/5051692/382cbd5e-ac3a-4b36-b5ad-bbc651a2a7a9',
          {
            fields: [{ name: 'email', value: this.email }],
          }
        )
        .then(x => {
          this.status = 'subscribed'
        })
        .catch(error => {
          console.log('Error:', error)
          this.submitted = false
        })
    },
  },
}
</script>

<style scoped>
body {
  font: bold 20px/1 Arial;
  color: #60718e;
}
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
}
img {
  width: 414px;
  max-width: 90%;
}
.zeugs {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 28px 20px;
}
ul {
  list-style-type: none;
}
small {
  max-width: 420px;
  margin-top: 12px;
  text-align: center;
  font: 12px/1.2 Arial;
}
small a {
  display: inline;
  text-decoration: underline;
  color: #60718e;
}
</style>
