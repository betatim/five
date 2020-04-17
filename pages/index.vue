<template>
  <div>
    <v-content>
      <v-container class="px-6 px-md-4">
        <script src="https://js.stripe.com/v3/" />
        <v-row justify="center">
          <v-col cols="12" sm="10" md="11" lg="9" xl="6">
            <div class="intro py-md-12 my-sm-4 my-md-12">
              <!-- Intro -->
              <h1
                :class="[
                  { 'display-1': $vuetify.breakpoint.smAndDown },
                  { 'display-4': $vuetify.breakpoint.mdAndUp },
                  'mb-6',
                ]"
              >
                Video-Identifikation für elektronisches Signieren mit höchster
                Beweiskraft
              </h1>
              <p
                :class="[
                  { 'font-weight-bold': $vuetify.breakpoint.smAndDown },
                  { headline: $vuetify.breakpoint.mdAndUp },
                  'mb-6',
                ]"
              >
                Erstellen Sie sich in wenigen Minuten eine E-ID, die das
                Signieren mit der qualifizierten elektronischen Signatur (QES)
                erlaubt. Die QES ist der höchste Signaturstandard und der
                handschriftlichen Unterschrift vor dem Gesetz gleichgestellt.
              </p>
              <p>
                Um Mit QES signieren zu können, muss man seine Identität
                einmalig überprüfen lassen. Bis am 02. Oktober 2020 Ist das per
                Video-Call möglich. Der Bund
                <a
                  class="link"
                  href="https://www.admin.ch/gov/de/start/dokumentation/medienmitteilungen.msg-id-78641.html"
                  target="_blank"
                  >setzte diese Ausnahmeregelung im Rahmen der COVID-19 Krise in
                  Kraft</a
                >, um die Notwendigkeit für persönlichen Kontakt zu reduzieren
                und der gestiegenen Nachfrage für elektronisches Signieren
                nachzukommen.
              </p>
              <p>
                Diese Verordnung gilt für den Rechtsraum Schweiz. Für das
                Signieren nach EU-Gesetz kann die E-ID auch nach dieser
                Zeitperiode weiter eingesetzt werden.
              </p>
              <p>
                VideoIdent.me wird von Skribble in Zusammenarbeit mit Swisscom
                und IdentityTM angeboten.
              </p>

              <div class="intro__logos my-6">
                <div class="intro__logo skribble-logo">
                  <img src="/logo-skribble.svg" alt="Skribble logo" />
                  <div>Skribble</div>
                </div>
                <div class="intro__logo identity-logo">
                  <img src="/identity-tm.png" alt="Identity.tm logo" />
                </div>
                <div class="intro__logo swisscom-logo">
                  <img
                    src="/swisscom-trust-services.png"
                    alt="Swisscom Trust Services logo"
                  />
                </div>
              </div>

              <v-btn
                @click="$vuetify.goTo('#pay-form')"
                class="mt-6"
                large
                color="primary"
                >Jetzt starten</v-btn
              >
            </div>
          </v-col>
        </v-row>
      </v-container>
      <v-container class="px-6 px-md-4">
        <v-row justify="center">
          <v-col cols="12" xl="9">
            <div class="steps py-2 py-md-12 my-2 my-md-12">
              <div
                :class="[
                  { 'text-center': $vuetify.breakpoint.smAndUp },
                  'steps__heading',
                ]"
              >
                <h2
                  :class="[
                    { 'display-1': $vuetify.breakpoint.smAndDown },
                    { 'display-3': $vuetify.breakpoint.mdAndUp },
                    'mb-6',
                  ]"
                >
                  In drei Schritten zur E-ID
                </h2>
                <p
                  :class="[
                    { 'font-weight-bold': $vuetify.breakpoint.smAndDown },
                    { headline: $vuetify.breakpoint.mdAndUp },
                  ]"
                >
                  Die Identitätsprüfung erfolgt online und dauert nur wenige
                  Minuten. Anschlissend wird die QES innert 30 Minuten für Sie
                  auf Skribble.com freigeschaltet.
                </p>
              </div>
              <ol class="steps__list mt-12 pa-0">
                <li>
                  <h3 class="headline">Mit Kreditkarte bezahlen</h3>
                  <p>
                    Sie brauchen keine Rechnung abzuwarten, um mit dem Signieren
                    loszulegen.
                  </p>
                </li>
                <li>
                  <h3 class="headline">Per Video-Call identifizieren lassen</h3>
                  <p>
                    Ein geschulter Mitarbeitender unseres
                    Identifikationspartners wird Ihr Identitätsdokument per
                    Webcam prüfen.
                  </p>
                </li>
                <li>
                  <h3 class="headline">Via Mobiltelefon bestätigen</h3>
                  <p>
                    Sie erhalten von Swisscom einen Link per SMS und legen das
                    Passwort fest, mit dem Sie in Zukunft ihre Signaturen
                    bestätigen.
                  </p>
                </li>
              </ol>
              <div class="steps__footer mt-12 text-center">
                <p>
                  Der Identifikationsservice ist täglich von 07.00 bis 22.00 Uhr
                  verfügbar.
                </p>
                <p>
                  Bitte halten Sie Ihren Reisepass/ID, eine Kreditkarte und Ihr
                  Mobiltelefon bereit. Ihr Gerät muss über eine Webcam und ein
                  Mikrofon verfügen.
                </p>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-container>

      <v-row id="pay-form" class="dark mx-0" justify="center">
        <v-col cols="12" sm="10" md="11" lg="9" xl="6">
          <div class="pay py-2 px-5 py-md-12 px-md-0 my-2 my-md-12">
            <div
              :class="[
                { 'text-center': $vuetify.breakpoint.smAndUp },
                'pay__heading',
              ]"
            >
              <h2
                :class="[
                  { 'display-1': $vuetify.breakpoint.smAndDown },
                  { 'display-3': $vuetify.breakpoint.mdAndUp },
                  'mb-6',
                  'white--text',
                ]"
              >
                Mit Kreditkarte bezahlen
              </h2>
              <p
                :class="[
                  { 'font-weight-bold': $vuetify.breakpoint.smAndDown },
                  { headline: $vuetify.breakpoint.mdAndUp },
                  'white--text',
                ]"
              >
                Nach dem Bezahlvorgang werden sie an unseren
                Identifikationspartner weitergeleitet, bei dem Sie sich im
                Auftrag von Swisscom Trust Services via Video-Call
                identifizieren können.
              </p>
            </div>
            <div class="pay__tag text-center mt-12 white--text">
              <strong
                >Sie profitieren für begrenzte Zeit vom Vorzugspreis von CHF
                19.-</strong
              ><br />
              (regulärer Preis: 25.-)
            </div>
            <!-- Form -->
            <div class="pay__flex">
              <v-card class="pay__card pa-6 my-12" outlined>
                <v-expand-transition>
                  <div
                    v-show="
                      status === 'start' || status === 'error-during-payment'
                    "
                    class="pay__form"
                  >
                    <v-form
                      ref="form"
                      v-model="validForm"
                      :lazy-validation="lazy"
                    >
                      <v-text-field
                        v-model="firstName"
                        :rules="nameRules"
                        label="Vorname"
                        autocomplete="given-name"
                        required
                        outlined
                      ></v-text-field>
                      <v-text-field
                        v-model="lastName"
                        :rules="nameRules"
                        label="Nachname"
                        autocomplete="family-name"
                        required
                        outlined
                      ></v-text-field>
                      <v-text-field
                        v-model="email"
                        :rules="emailRules"
                        label="E-Mail"
                        autocomplete="email"
                        required
                        outlined
                      ></v-text-field>

                      <card
                        class="stripe-card"
                        :class="{ complete: completeStripe }"
                        :stripe="stripe_pk"
                        :options="stripeOptions"
                        @change="completeStripe = $event.complete"
                      />
                      <v-checkbox
                        class="pay__consent mt-8 mx-auto"
                        v-model="checkbox"
                        :rules="[
                          v =>
                            !!v ||
                            'Sie müssen zustimmen, um den Prozess zu starten.',
                        ]"
                        required
                      >
                        <template v-slot:label>
                          <div class="pay__consent-label">
                            Mit dem Bezahlen akzeptiere ich Skribbles
                            <a
                              @click.stop
                              class="link"
                              href="https://www.skribble.com/de/datenschutz/"
                              target="_blank"
                              >Datenschutzrichtlinien</a
                            >.
                          </div>
                        </template>
                      </v-checkbox>
                      <div class="text-center mt-6">
                        <v-btn
                          @click="pay"
                          large
                          class="pay-with-stripe"
                          color="primary"
                          :disabled="!(validForm && completeStripe)"
                        >
                          Jetzt bezahlen
                        </v-btn>
                      </div>

                      <!-- Error during payment -->
                      <div
                        class="text-center mt-4"
                        v-if="status === 'error-during-payment'"
                      >
                        <p
                          v-if="stripePaymentErrorMsg !== ''"
                          class="caption red--text"
                        >
                          {{ stripePaymentErrorMsg }}
                        </p>
                        <p class="caption red--text">
                          Es ist ein Fehler beim Bezahlen aufgetreten. Bitte
                          verwenden Sie ein anderes Zahlungsmittel oder
                          versuchen Sie es später erneut.
                        </p>
                      </div>
                    </v-form>
                  </div>
                </v-expand-transition>

                <!-- Error after payment -->
                <div
                  v-if="status === 'error-after-payment'"
                  class="pay__error text--text text-center"
                >
                  <p>
                    Die Zahlung war erfolgreich, aber wir konnten keinen
                    Identifikationsprozess erstellen. Klicken Sie auf Erneut
                    senden, um es nochmals zu versuchen.
                  </p>
                  <p>
                    Ihre Karte wird nicht nochmals belastet.
                  </p>
                  <div class="mt-10 text-center">
                    <v-btn large color="primary" @click="reSubmit">
                      Erneut senden
                    </v-btn>
                  </div>
                </div>

                <!-- Spinner Overlay -->
                <v-expand-transition>
                  <div v-show="status === 'processing'" class="text-center">
                    <v-progress-circular
                      indeterminate
                      color="primary"
                    ></v-progress-circular>
                  </div>
                </v-expand-transition>

                <!-- Success -->
                <v-expand-transition>
                  <div
                    v-show="status === 'paid'"
                    class="pay__success pa-4 text--text text-center"
                  >
                    <h2
                      :class="[
                        { 'display-1': $vuetify.breakpoint.smAndDown },
                        { 'display-3': $vuetify.breakpoint.mdAndUp },
                        'mb-6',
                      ]"
                    >
                      Zahlung erfolgreich!
                    </h2>
                    <p>
                      Die Bestätigung finden Sie in Ihrem E-Mail-Briefkasten.
                    </p>
                    <v-btn
                      large
                      color="primary"
                      class="mt-6 mb-10"
                      :href="identURL"
                      target="_blank"
                    >
                      Video-Identifikation jetzt starten
                    </v-btn>
                    <p class="caption mb-0">
                      Sie werden zum Portal unseres Identifikations-Partners
                      weitergeleitet, bei dem Sie sich im Auftrag der Swisscom
                      Trust Services identifizieren können. Ihre hierfür
                      erhobenen Personendaten werden ausschliesslich für die
                      ordnungsgemässe Identifizierung im Rahmen der
                      elektronischen Signatur verwendet.
                    </p>
                  </div>
                </v-expand-transition>
              </v-card>
            </div>
          </div>
        </v-col>
      </v-row>

      <v-container class="px-6 px-md-4">
        <v-row justify="center">
          <v-col cols="12" sm="10" md="11" lg="9" xl="6">
            <div class="faq py-2 py-md-12 my-2 my-md-12">
              <!-- FAQ -->
              <h2 class="display-3 mb-6 text-center">FAQ</h2>
              <v-expansion-panels accordion flat multiple class="my-10">
                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Was passiert mit der E-ID nach dem 2. Oktober 2020?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content>
                    Die hier erstellt E-ID wird, nach heutigem Kenntnisstand,
                    per 2. Oktober 2020 fürs Signieren nach Schweizer Gesetz
                    (ZertES) deaktiviert werden müssen. Die E-ID kann jedoch
                    weiterhin fürs Signieren nach europäischen Gesetzt (eIDAS)
                    eingesetzt werden.</v-expansion-panel-content
                  >
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Wo wird meine E-ID gespeichert?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Die E-ID wird nach höchsten Sicherheitsstandards,
                    verschlüsselt in den Rechenzentren der Swisscom abgelegt.
                    Die E-ID kann nur im Falle eines Rechtsfalls von den
                    Sicherheitsleuten des Swisscom Signing Service im
                    4-Augen-Prinzip entschlüsselt und den Behörden zur Verfügung
                    gestellt werden.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Für was kann ich die E-ID alles nutzen?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content>
                    Die hier erstellte E-ID wird in erster Linie für das
                    Signieren mit der Qualifizierten Elektronischen Signatur
                    (QES) generiert. Falls Sie sich für andere Anwendungsfälle
                    interessieren, kontaktieren Sie bitte Skribble.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Wer führt die Video-Identifikation durch?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content>
                    Die Identifikation wird von Swisscom Trust Services
                    angeboten und in Zusammenarbeit mit identity Trust
                    Management AG durchgeführt.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Ich bin nicht aus der Schweiz. Kann ich mich trotzdem
                    identifizieren lassen?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Ja, der Service steht für die meisten Nationalitäten zur
                    Verfügung.
                    <a
                      class="link"
                      href="http://documents.swisscom.com/product/filestore/lib/5705ba58-3fdb-446f-9e48-18a297b8d239/l%C3%A4nderliste%20f%C3%BCr%20die%20videoidentifikation-kurier-pos-en.pdf?idxme=pex-search"
                      target="_blank"
                      >Liste der akzeptierten Länder und Ausweisdokumente
                      ansehen.</a
                    >
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Wie lange dauert, bis ich die E-ID für das Signieren
                    einsetzen kann?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Die QES wird nach maximal 30 Minuten nach der
                    Identifikation auf Skribble und anderen Services, die auf
                    Swisscom Signing Service beruhenden, freigeschaltet.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Wie lange dauert die Video-Identifikation?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Die Video-Identifikation dauert ca. 5 Minuten. Je nach
                    Auslastung des Video-Identifikations-Team kann die Wartezeit
                    bis zum Start der Videoidentifikation bis zu 2 Minuten
                    betragen.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    In welcher Sprache kann ich die Video-Identifikation
                    durchführen?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Du kannst die Identifikation in Deutsch und Englisch
                    durchführen.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header
                    >Was ist im Preis enthalten?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Im Preis enthalten ist die Identifikation via Video, die
                    anschliessend generierte elektronische Identität (E-ID).
                    Nicht enthalten sind die Signaturen, die mit der E-ID
                    gemacht werden.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Für welche Signaturservices kann ich die E-ID einsetzen?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content>
                    Die E-ID kann für Skribble und andere Signaturservices
                    eingesetzt werden, die auf Swisscom Signing Service
                    beruhenden.
                  </v-expansion-panel-content>
                </v-expansion-panel>

                <v-expansion-panel>
                  <v-expansion-panel-header>
                    Ist mein Signaturpasswort auf allen Signaturservices
                    dasselbe?
                  </v-expansion-panel-header>
                  <v-expansion-panel-content
                    >Ja. Ihr Passwort ist an Ihre E-ID geknüpft und kommt immer
                    zum Zug, wenn sie mit einem Anbieter signieren, der auf dem
                    Swisscom Signing Service beruht.
                  </v-expansion-panel-content>
                </v-expansion-panel>
              </v-expansion-panels>
            </div>
          </v-col>
        </v-row>
      </v-container>
      <v-container class="px-6 px-md-4">
        <v-row justify="center">
          <div class="footer text-center my-10">
            Built by
            <div class="skribble-logo mt-2">
              <img src="/logo-skribble.svg" alt="Skribble logo" />
              <div>Skribble</div>
            </div>
          </div>
        </v-row>
      </v-container>
    </v-content>
  </div>
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
          fonts: [
            {
              family: 'Averta',
              src:
                'url("https://my.skribble.com/_nuxt/fonts/48cfe38.woff2") format("woff2")',
              style: 'normal',
              weight: 400,
              display: 'swap',
            },
          ],
        },
        style: {
          base: {
            color: '#293D66',
            fontSize: '20px',
            fontFamily: 'Averta',
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
      nameRules: [v => !!v || 'Name wird benötigt'],
      email: '',
      emailRules: [
        v => !!v || 'E-mail wird benötigt',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      checkbox: false,
      lazy: false,

      paymentIntentID: '',
      identURL: '',
      stripePaymentErrorMsg: '',
    }
  },

  components: { Card },
  methods: {
    pay() {
      this.status = 'processing'
      this.stripePaymentErrorMsg = ''

      // Async functions must be defined as arrow function so we can still scope Vue's "this"

      // Call Seven (our backend) to setup a payment event
      const setupPaymentIntent = async () => {
        try {
          return await this.$axios.$post('/api/setup_payment', {
            email: this.email,
          })
        } catch (error) {
          this.status = 'error-during-payment'
          throw error
        }
      }

      // Call Stripe to create a payment method
      const createPaymentMethodInStripe = async () => {
        try {
          return await createPaymentMethod('card', {})
        } catch (error) {
          this.status = 'error-during-payment'
          throw error
        }
      }

      // Call Stripe to execute payment
      const handleCardPaymentInStripe = async (clientSecret, paymentMethod) => {
        try {
          const response = await handleCardPayment(clientSecret, paymentMethod)
          if ('error' in response) throw response.error

          // store formatted paymentIntentID so we can use it in other methods
          this.paymentIntentID = response.paymentIntent.id.replace('pi_', '')
        } catch (error) {
          this.status = 'error-during-payment'
          this.stripePaymentErrorMsg = error.message
          throw error
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
          throw error
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

<style lang="sass">
@import ~/assets/sass/_vars
@import ~/assets/sass/_mixins

.skribble-logo
  display: flex
  align-items: center
  font: bold 1.5rem/1 $averta
  color: $c-skribbleu

  img
    margin-right: 2px

.identity-logo img
  width: 150px
  max-width: 100%

.swisscom-logo img
  width: 242px
  max-width: 100%

.dark
  background-color: $c-skribbleu

.intro
  margin-left: auto
  margin-right: auto
  max-width: 680px

  &__logos
    display: flex
    align-items: center
    +media(sm-and-down)
      flex-direction: column
      align-items: flex-start

  &__logo
    margin: 0 20px
    +media(sm-and-down)
      margin: 10px
    +media(md-and-up)
      &:first-child
        margin-left: 0
      &:last-child
        margin-right: 0

.steps

  &__heading
    margin-left: auto
    margin-right: auto
    max-width: 480px

  &__footer
    margin-left: auto
    margin-right: auto
    max-width: 680px

  &__list
    display: flex
    justify-content: center
    margin: 0
    list-style-type: none
    +media(sm-and-down)
      flex-wrap: wrap

    li
      flex: 0 1 31.33%
      margin: 0 2%
      padding-bottom: 10px
      background-color: #fff
      box-shadow: 0 1px 10px 0 rgba($c-grey-darker, .3)
      +media(sm-and-down)
        flex: 0 1 100%
        margin: 0
      @for $i from 1 through 3
        &:nth-child(#{$i})
          +media(sm-and-down)
            @if $i == 2
              margin: 40px 0
          h3:after
            content: '#{$i}'

    h3
      display: flex
      justify-content: space-between
      align-items: center
      &:after
        flex-basis: 20%
        font-size: 1.9rem
        text-align: right

    .headline
      padding: 20px
      margin-bottom: 20px
      border-bottom: 1px solid $c-border

    p
      margin: 10px 20px

.pay

  .stripe-card
    padding: 15px 8px
    border: 1px solid rgba(0,0,0,.38)
    border-radius: 4px

  &__heading
    margin-left: auto
    margin-right: auto
    max-width: 480px

  &__tag
    margin-left: auto
    margin-right: auto
    max-width: 600px
    padding: 20px 0
    border-top: 1px solid #fff
    border-bottom: 1px solid #fff

  &__consent.v-input
    max-width: 300px

  &__card.v-card
    max-width: 580px
    margin-left: auto
    margin-right: auto

  &__form
    max-width: 580px

  &__success
    max-width: 580px

  &__error
    max-width: 580px

.faq

  .theme--light.v-expansion-panels .v-expansion-panel
    color: $c-text

  .v-expansion-panel
    border-bottom: 1px solid $c-border
    &:first-child
      border-top: 1px solid $c-border

    &-header
      padding: 16px 36px 16px 0
      font: bold 1rem/1.4 $averta
      color: $c-skribbleu

    &-content__wrap
      max-width: 700px
      padding-left: 0

.footer
  font-size: .8rem

  .skribble-logo
    font: bold 1.5rem/1 $averta
    color: $c-skribbleu
</style>
