<template>
  <div>
    <!-- Intro -->
    <h1>Get your E-ID now!</h1>
    <h2>Faster than ever</h2>
    <p>
      Explain what this is, link to/quote from Bundesrat announcement, what
      will happen if you use this, etc. Text to make the user feel
      comfortable and happy to use this page. Mention price.
      <a href="#">Link to sources</a>
    </p>
    <h2>Ready in only 3 steps</h2>
    <ol>
      <li>
        <h3>Pay</h3>
        <p>That's right. Money first, you know the drill.</p>
      </li>
      <li>
        <h3>Video Ident</h3>
        <p>Quick and easy - with our partners. <a href="#">Link to nowhere</a></p>
      </li>
      <li>
        <h3>Ready to sign</h3>
        <p>Automatically connected with your Skribble account. Log in and start signing like there's no tomorrow.</p>
      </li>
    </ol>
    
    <!-- Form -->
    <v-card class="mx-auto pa-4 my-10" max-width="600" outlined>
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

      <!-- Overlay -->
      <div v-show="status === 'paying'" class="text-center">
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

    <!-- FAQ -->
    <v-expansion-panels class="my-10">
      <v-expansion-panel>
        <v-expansion-panel-header>Was passiert mit der ID nach dem 1. Okt 2020?</v-expansion-panel-header>
        <v-expansion-panel-content>Lorem ipsum dolor sit amet consectetur adipisicing elit. Accusantium laboriosam amet ducimus enim <a href="#">Link to somewhere</a> itaque ipsum quas fugiat repudiandae ex atque corporis cupiditate aperiam, quidem consequuntur minima sunt? Nisi, eligendi aperiam.</v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>Wer ist der VideoIdent Anbieter?</v-expansion-panel-header>
        <v-expansion-panel-content>
          <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Blanditiis ullam dolorem optio nihil, <strong>magnam minima ipsam, maiores ex deleniti eius</strong>, possimus id! Sint ex ad doloribus qui illo, nostrum velit.</p>
          <ul>
            <li>Number 1</li>
            <li>Number 2</li>
            <li>Number 3</li>
          </ul>
          <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Hic nesciunt placeat harum blanditiis accusamus culpa esse minus sint exercitationem, quod quasi dicta quidem tempora nemo explicabo vitae! Sit, laudantium exercitationem.</p>
          <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Hic nesciunt placeat harum blanditiis accusamus culpa esse minus sint exercitationem, quod quasi dicta quidem tempora nemo explicabo vitae! Sit, laudantium exercitationem.</p>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>Welche Dokumente kann ich für die Identifikation verwenden?</v-expansion-panel-header>
        <v-expansion-panel-content>Lorem ipsum dolor sit amet consectetur, adipisicing elit. <em>Blanditiis ullam dolorem optio nihil</em>, magnam minima ipsam, maiores ex deleniti eius, possimus id! Sint ex ad doloribus qui illo, nostrum velit.</v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>

    <!-- Disclaimer -->
    <div class="text-center my-10">
      Built by Skribble <img src="/logo-skribble.svg" alt />
    </div>
  </div>
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
