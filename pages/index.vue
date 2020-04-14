<template>
  <v-container>
    <script src="https://js.stripe.com/v3/" />
    <v-row justify="center">
      <v-col cols="12" sm="10" md="11" lg="9" xl="6">
        <!-- Intro -->
        <h1>
          Video-Identifikation für elektronisches Signieren mit höchster
          Beweiskraft
        </h1>
        <h2>
          Erstellen Sie sich in wenigen Minuten eine E-ID, die das Signieren mit
          der qualifizierten elektronischen Signatur (QES) erlaubt. Die QES ist
          der höchste Signaturstandard und der handschriftlichen Unterschrift
          vor dem Gesetz gleichgestellt.
        </h2>
        <p>
          Um Mit QES signieren zu können, muss man seine Identität einmalig
          überprüfen lassen. Bis am 02. Oktober 2020 Ist das per Video-Call
          möglich. Der Bund setzte diese Ausnahmeregelung im Rahmen der COVID-19
          Krise in Kraft, um die Notwendigkeit für persönlichen Kontakt zu
          reduzieren und der gestiegenen Nachfrage für elektronisches Signieren
          nachzukommen.
          <a href="#">Link to sources</a>
        </p>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" sm="10" md="11" lg="9" xl="6">
        <h2>Ready in only 3 steps</h2>
        <ol>
          <li>
            <h3>Pay</h3>
            <p>That's right. Money first, you know the drill.</p>
          </li>
          <li>
            <h3>Video Ident</h3>
            <p>
              Quick and easy - with our partners.
              <a href="#">Link to nowhere</a>
            </p>
          </li>
          <li>
            <h3>Ready to sign</h3>
            <p>
              Automatically connected with your Skribble account. Log in and
              start signing like there's no tomorrow.
            </p>
          </li>
        </ol>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" sm="10" md="11" lg="9" xl="6">
        <!-- Form -->
        <v-card class="mx-auto pa-4 my-10" max-width="600" outlined>
          <v-form
            v-show="status === 'start' || status === 'error-during-payment'"
            ref="form"
            v-model="validForm"
            :lazy-validation="lazy"
          >
            <v-text-field
              v-model="firstName"
              :counter="20"
              :rules="nameRules"
              label="First Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="lastName"
              :counter="20"
              :rules="nameRules"
              label="Last Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-mail"
              required
            ></v-text-field>

            <card
              class="stripe-card ma-4"
              :class="{ complete: completeStripe }"
              :stripe="stripe_pk"
              :options="stripeOptions"
              @change="completeStripe = $event.complete"
            />

            <v-checkbox
              v-model="checkbox"
              :rules="[v => !!v || 'You must agree to continue!']"
              label="Do you agree?"
              required
            ></v-checkbox>
            <div class="text-center">
              <v-btn
                class="pay-with-stripe"
                @click="pay"
                :disabled="!(validForm && completeStripe)"
              >
                Pay now
              </v-btn>
            </div>

            <!-- Error during payment -->
            <p
              v-if="status === 'error-during-payment'"
              class="caption red--text mt-3"
            >
              There was an error while processing your payment. Please use a
              different payment method or try again later
            </p>
          </v-form>

          <!-- Error after payment -->
          <div v-if="status === 'error-after-payment'">
            <p>
              Your payment was processed successfully but there was an error
              while generating your identification request.
            </p>
            <p>
              Click below to re-submit your information. You will not be charged
              again.
            </p>
            <div class="text-center">
              <v-btn @click="reSubmit">
                Re-submit
              </v-btn>
            </div>
          </div>

          <!-- Spinner Overlay -->
          <div v-show="status === 'processing'" class="text-center">
            <v-progress-circular
              indeterminate
              color="primary"
            ></v-progress-circular>
          </div>

          <!-- Success -->
          <div v-show="status === 'paid'">
            <p>Your e-ID video ident appointment is now ready for you.</p>
            <p>
              Visit the link below to start it now (opens a new tab):
              <a :href="identURL" target="_blank">{{ identURL }}</a>
            </p>
            <p>We sent you a receipt for your payment by email.</p>
            <p>Platforms to use your eID with:</p>
            <ul>
              <li>Skribble</li>
              <li>Many more (link to SC list of other?)></li>
            </ul>
          </div>
        </v-card>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" sm="10" md="11" lg="9" xl="6">
        <!-- FAQ -->
        <v-expansion-panels class="my-10">
          <v-expansion-panel>
            <v-expansion-panel-header
              >Was passiert mit der ID nach dem 1. Okt
              2020?</v-expansion-panel-header
            >
            <v-expansion-panel-content
              >Lorem ipsum dolor sit amet consectetur adipisicing elit.
              Accusantium laboriosam amet ducimus enim
              <a href="#">Link to somewhere</a> itaque ipsum quas fugiat
              repudiandae ex atque corporis cupiditate aperiam, quidem
              consequuntur minima sunt? Nisi, eligendi
              aperiam.</v-expansion-panel-content
            >
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header
              >Wer ist der VideoIdent Anbieter?</v-expansion-panel-header
            >
            <v-expansion-panel-content>
              <p>
                Lorem ipsum dolor sit amet consectetur, adipisicing elit.
                Blanditiis ullam dolorem optio nihil,
                <strong>magnam minima ipsam, maiores ex deleniti eius</strong>,
                possimus id! Sint ex ad doloribus qui illo, nostrum velit.
              </p>
              <ul>
                <li>Number 1</li>
                <li>Number 2</li>
                <li>Number 3</li>
              </ul>
              <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit. Hic
                nesciunt placeat harum blanditiis accusamus culpa esse minus
                sint exercitationem, quod quasi dicta quidem tempora nemo
                explicabo vitae! Sit, laudantium exercitationem.
              </p>
              <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit. Hic
                nesciunt placeat harum blanditiis accusamus culpa esse minus
                sint exercitationem, quod quasi dicta quidem tempora nemo
                explicabo vitae! Sit, laudantium exercitationem.
              </p>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header
              >Welche Dokumente kann ich für die Identifikation
              verwenden?</v-expansion-panel-header
            >
            <v-expansion-panel-content
              >Lorem ipsum dolor sit amet consectetur, adipisicing elit.
              <em>Blanditiis ullam dolorem optio nihil</em>, magnam minima
              ipsam, maiores ex deleniti eius, possimus id! Sint ex ad doloribus
              qui illo, nostrum velit.</v-expansion-panel-content
            >
          </v-expansion-panel>
        </v-expansion-panels>

        <!-- Disclaimer -->
        <div class="text-center my-10">
          Built by Skribble <img src="/logo-skribble.svg" alt />
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import {
  Card,
  createPaymentMethod,
  handleCardPayment,
} from 'vue-stripe-elements-plus'

export default {
  data() {
    return {
      status: 'start',
      completeStripe: false,
      stripe_pk: process.env.strPk,
      stripeOptions: {
        // see https://stripe.com/docs/stripe.js#element-options for details
        elements: {
          // fonts: [
          //   {
          //     family: "Averta",
          //     src:
          //       'url("https://my.skribble.com/_nuxt/fonts/48cfe38.woff2") format("woff2")',
          //     style: "normal",
          //     weight: 400,
          //     display: "swap",
          //   },
          // ],
        },
        style: {
          base: {
            color: '#293D66',
            fontSize: '18px',
            fontFamily: 'Roboto',
            fontSmoothing: 'antialiased',
            '::placeholder': {
              color: '#65728E',
            },
          },
        },
      },

      validForm: true,
      firstName: '',
      lastName: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Names must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      checkbox: false,
      lazy: false,

      paymentIntentID: '',
      identURL: '',
    }
  },

  components: { Card },
  methods: {
    pay() {
      this.status = 'processing'

      // Async functions must be defined as arrow function so we can still scope Vue's "this"

      // Call Seven (our backend) to setup a payment event
      const setupPaymentIntent = async () => {
        try {
          return await this.$axios.$post('/api/setup_payment', {
            email: this.email,
          })
        } catch (error) {
          this.status = 'error-during-payment'
        }
      }

      // Call Stripe to create a payment method
      const createPaymentMethodInStripe = async () => {
        try {
          return await createPaymentMethod('card', {})
        } catch (error) {
          this.status = 'error-during-payment'
        }
      }

      // Call Stripe to execute payment
      const handleCardPaymentInStripe = async (clientSecret, paymentMethod) => {
        try {
          const response = await handleCardPayment(clientSecret, paymentMethod)
          if (response.paymentIntent.status !== 'succeeded')
            throw 'Payment intent failed'
          // store formatted paymentIntentID so we can use it in other methods
          this.paymentIntentID = response.paymentIntent.id.replace('pi_', '')
        } catch (error) {
          this.status = 'error-during-payment'
        }
      }

      // Call Seven (our backend) to create an identity request
      const createIdentityRequest = async () => {
        try {
          return await this.$axios.$post(
            `/api/create_ident/${this.paymentIntentID}`,
            {
              firstName: this.firstName,
              lastName: this.lastName,
            }
          )
        } catch (error) {
          this.status = 'error-after-payment'
        }
      }

      // Call our backend to setup a payment intent and Stripe to create a payment method
      Promise.all([setupPaymentIntent(), createPaymentMethodInStripe()]).then(
        ([responsePaymentIntent, responsePaymentMethod]) => {
          // Once result from both is received, execute payment with Stripe
          handleCardPaymentInStripe(
            responsePaymentIntent.clientSecret,
            responsePaymentMethod.createPaymentMethod
          ).then(responseHandlePayment => {
            // Once response from Stripe is received, call our backend to create an identity request
            createIdentityRequest().then(responseIdentityRequest => {
              // Once result from the identity request is received, set ident url to show the user where to go
              this.identURL = responseIdentityRequest.identUrl
              this.status = 'paid'
            })
          })
        }
      )
    },
    reSubmit() {
      this.status = 'processing'

      // Call Seven (our backend) to create an identity request
      const createIdentityRequest = async () => {
        try {
          return await this.$axios.$post(
            `/api/create_ident/${this.paymentIntentID}`,
            {
              firstName: this.firstName,
              lastName: this.lastName,
            }
          )
        } catch (error) {
          this.status = 'error-after-payment'
        }
      }

      // Call Seven to start an identity creation request
      createIdentityRequest().then(responseIdentityRequest => {
        // Once result from the identity request is received, set ident url to show the user where to go
        this.identURL = responseIdentityRequest.identUrl
        this.status = 'paid'
      })
    },
  },
}
</script>
