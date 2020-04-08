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
        <v-card class="mx-auto pa-4" max-width="600" outlined
          ><div v-show="status === 'paying'" class="text-center">
            <v-progress-circular
              indeterminate
              color="primary"
            ></v-progress-circular>
          </div>
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
          <v-card-actions> </v-card-actions>
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
  createToken,
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
      firstName: "Name",
      lastName: "Surname",
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => (v && v.length <= 10) || "Names must be less than 10 characters",
      ],
      email: "namesurname@protonmail.com",
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
      ],
      checkbox: true,
      lazy: false,
    };
  },

  components: { Card },
  beforeCreate() {
    // Get stripe public key from backend
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
      // createToken returns a Promise which resolves in a result object with
      // either a token or an error key.
      // See https://stripe.com/docs/api#tokens for the token object.
      // See https://stripe.com/docs/api#errors for the error object.
      // More general https://stripe.com/docs/stripe.js#stripe-create-token.
      //
      this.$axios
        .$post("/api/setup_payment", {
          email: this.email,
        })
        .then((response) => {
          createPaymentMethod("card", {}).then((response2) => {
            handleCardPayment(
              response.clientSecret,
              response2.createPaymentMethod
            ).then((response3) => {
              if (response3.paymentIntent.status === "succeeded") {
                const paymentIntentID = response3.paymentIntent.id.replace(
                  "pi_",
                  ""
                );
                this.$axios
                  .$post(`/api/create_ident/${paymentIntentID}`, {
                    firstName: this.firstName,
                    lastName: this.lastName,
                  })
                  .then((response4) => console.log(response4));
              } else console.error("payment failed");
            });
          });
        });
    },
  },
};
</script>
