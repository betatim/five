<template>
  <v-layout>
    <script src="https://js.stripe.com/v3/" />
    <v-row align="center" justify="center"
      ><v-col cols="12" sm="10" md="6">
        <p class="title">Get your E-ID now!</p>
        <p>
          Explain what this is, link to/quote from Bundesrat announcement, what
          will happen if you use this, etc. Text to make the user feel
          comfortable and happy to use this page. Mention price.
        </p>
        <v-row align="center" justify="center"></v-row>
        <v-card class="mx-auto pa-4" max-width="600" outlined>
          <v-form
            v-show="status === 'start'"
            ref="form"
            v-model="valid"
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
              v-if="stripe_pk"
              class="stripe-card ma-4"
              :class="{ complete }"
              :stripe="stripe_pk"
              :options="stripeOptions"
              @change="complete = $event.complete"
            />

            <v-checkbox
              v-model="checkbox"
              :rules="[(v) => !!v || 'You must agree to continue!']"
              label="Do you agree?"
              required
            ></v-checkbox>

            <v-btn class="pay-with-stripe" @click="pay" :disabled="!valid">
              Pay now
            </v-btn>
          </v-form>
          <div v-show="status === 'paying'" class="text-center">
            <v-progress-circular
              indeterminate
              color="primary"
            ></v-progress-circular>
          </div>
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

        <div class="text-center">
          Built by Skribble <img src="/logo-skribble.svg" alt />
        </div>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
import {
  Card,
  createPaymentMethod,
  handleCardPayment,
} from "vue-stripe-elements-plus";

export default {
  data() {
    return {
      status: "start",
      complete: false,
      stripe_pk: null,
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
            color: "#293D66",
            fontSize: "18px",
            fontFamily: "Roboto",
            fontSmoothing: "antialiased",
            "::placeholder": {
              color: "#65728E",
            },
          },
        },
      },

      valid: true,
      firstName: "",
      lastName: "",
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => (v && v.length <= 10) || "Names must be less than 10 characters",
      ],
      email: "",
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
      ],
      checkbox: false,
      lazy: false,

      identURL: "",
    };
  },

  components: { Card },
  beforeCreate() {
    // Get stripe public key from backend. The Stripe element needs that key before it is loaded
    this.$axios
      .$post("/api/setup_payment", {
        email: "joe@example.com",
      })
      .then((response) => {
        this.stripe_pk = response.publishableKey;
      });
  },
  methods: {
    pay() {
      this.status = "paying";

      // Call Seven to get clientSecret
      this.$axios
        .$post("/api/setup_payment", {
          email: this.email,
        })
        .then((response) => {
          // Create a payment method with the data that the user entered in the stripe element
          createPaymentMethod("card", {}).then((response2) => {
            // Call Stripe to handle payment
            handleCardPayment(
              response.clientSecret,
              response2.createPaymentMethod
            ).then((response3) => {
              // If payment succeeded
              if (response3.paymentIntent.status === "succeeded") {
                const paymentIntentID = response3.paymentIntent.id.replace(
                  "pi_",
                  ""
                );
                // Call Seven to start an identity creation request
                this.$axios
                  .$post(`/api/create_ident/${paymentIntentID}`, {
                    firstName: this.firstName,
                    lastName: this.lastName,
                  })
                  .then((response4) => {
                    // Set url to show the user where to go
                    this.identURL = response4.identUrl;
                    this.status = "paid";
                  });
              } else console.error("payment failed");
            });
          });
        });
    },
  },
};
</script>
