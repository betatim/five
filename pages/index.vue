<template>
  <div>
    <v-content>
      <v-container class="px-6 px-md-4">
        <script src="https://js.stripe.com/v3/" />
        <v-row justify="center">
          <v-col cols="12" sm="10" md="11" lg="9" xl="6">
            <div class="intro py-0 py-md-12 my-0 my-sm-4 my-md-12">
              <!-- Intro -->
              <h1
                :class="[
                  { 'display-1': breakpoint.smAndDown },
                  { 'display-4': breakpoint.mdAndUp },
                  'mb-6',
                ]"
              >
                {{ $t('intro.title') }}
              </h1>
              <p
                :class="[
                  { 'font-weight-bold': breakpoint.smAndDown },
                  { headline: breakpoint.mdAndUp },
                  'mb-6',
                ]"
                v-html="$t('intro.subtitle')"
              ></p>
              <p v-html="$t('intro.content.paragraph1')"></p>

              <div class="intro__logos my-6">
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
              <div class="text-center">
                <v-btn
                  @click="$vuetify.goTo('#pay-form')"
                  class="intro__cta mt-md-6"
                  large
                  color="primary"
                  :block="breakpoint.xsOnly"
                  >{{ $t('intro.cta') }}</v-btn
                >
              </div>
            </div>
          </v-col>
        </v-row>
      </v-container>
      <v-container class="px-6 px-md-4">
        <v-row justify="center">
          <v-col cols="12" xl="9">
            <div class="steps py-2 py-md-12 my-4 my-md-12">
              <div
                :class="[
                  { 'text-center': breakpoint.smAndUp },
                  { 'mx-auto': breakpoint.smAndUp },
                  'steps__heading',
                ]"
              >
                <h2
                  :class="[
                    { 'display-1': breakpoint.smAndDown },
                    { 'display-3': breakpoint.mdAndUp },
                    'mb-6',
                  ]"
                >
                  {{ $t('steps.title') }}
                </h2>
                <p
                  :class="[
                    { 'font-weight-bold': breakpoint.smAndDown },
                    { headline: breakpoint.mdAndUp },
                  ]"
                  v-html="$t('steps.subtitle')"
                ></p>
              </div>

              <ol class="steps__list mt-8 mt-md-12 pa-0">
                <li>
                  <h3 class="headline">{{ $t('steps.step1.title') }}</h3>
                  <p>{{ $t('steps.step1.description') }}</p>
                </li>
                <li>
                  <h3 class="headline">{{ $t('steps.step2.title') }}</h3>
                  <p>{{ $t('steps.step2.description') }}</p>
                </li>
                <li>
                  <h3 class="headline">{{ $t('steps.step3.title') }}</h3>
                  <p>{{ $t('steps.step3.description') }}</p>
                </li>
              </ol>
              <div
                :class="[
                  { 'text-center': $vuetify.breakpoint.smAndUp },
                  'steps__footer',
                  'mt-8 mt-md-12',
                ]"
              >
                <p>{{ $t('steps.caption.paragraph1') }}</p>
                <p>{{ $t('steps.caption.paragraph2') }}</p>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-container>

      <the-payment-form />

      <the-f-a-q />

      <v-container class="px-6 px-md-4">
        <!-- Temporary language switcher, to be replaced as soon as we have multi-region -->
        <!-- Disabled until VideoIdent works in English -->
        <!-- <v-row justify="center">
          <div class="footer text-center my-5">
            <div v-if="$i18n.locale === 'ch/de'">
              <strong>Deutsch</strong> |
              <nuxt-link
                :to="switchLocalePath('ch/en')"
                class="link"
                style="text-decoration: none;"
                >English</nuxt-link
              >
            </div>
            <div v-if="$i18n.locale === 'ch/en'">
              <nuxt-link
                :to="switchLocalePath('ch/de')"
                class="link"
                style="text-decoration: none;"
                >Deutsch</nuxt-link
              >
              |
              <strong>English</strong>
            </div>
          </div>
        </v-row> -->
        <v-row justify="center">
          <div class="footer text-center my-5">
            {{ $t('footer.built_by') }}
            <a
              :href="$t('global.skribbleURL')"
              target="_blank"
              class="skribble-logo mt-2"
            >
              <img src="/logo-skribble.svg" alt="Skribble logo" />
              <div>Skribble</div>
            </a>
          </div>
        </v-row>
      </v-container>
    </v-content>
  </div>
</template>

<script>
import TheFAQ from '~/components/TheFAQ.vue'
import ThePaymentForm from '~/components/ThePaymentForm.vue'

export default {
  components: { TheFAQ, ThePaymentForm },
  data() {
    return {
      isMounted: false,
      initialWidth: 960, // Most (+-60%) users are using screen sizes of 960 and above
    }
  },
  computed: {
    breakpoint() {
      // Vuetify takes some time to calculate the initial breakpoints and associated service object variables.
      // In order to avoid FOUC (flash of unstyled content) we manually hardcode the initial breakpoint variables

      // Initial variables. Only the variables used in the template are specified.
      // The breakpoints correspond to ~/assets/variables.sass
      const initialBreakPointVariables = {
        xsOnly: this.initialWidth < 600,
        smAndDown: this.initialWidth < 960,
        smAndUp: this.initialWidth >= 600,
        mdAndUp: this.initialWidth >= 960,
      }

      // If templated has finished mounting, use real variables. Until then, use initial variables
      return this.isMounted
        ? this.$vuetify.breakpoint
        : initialBreakPointVariables
    },
  },
  beforeMount() {
    this.initialWidth = window.innerWidth
  },
  mounted() {
    this.isMounted = true
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
  margin-top: 48px
  margin-bottom: 48px
  padding-top: 48px
  padding-bottom: 48px

  &__logos
    display: flex
    align-items: center
    justify-content: center
    height: 35px
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

  &__cta.v-btn:not(.v-btn--round).v-size--large
    min-width: 240px

.steps
  margin-top: 48px
  margin-bottom: 48px
  padding-top: 48px
  padding-bottom: 48px

  &__heading
    max-width: 480px

    a
      color: $c-skribbleu

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
              margin: 24px 0
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

.footer
  font-size: .8rem

  .skribble-logo
    font: bold 1.5rem/1 $averta
    color: $c-skribbleu

  a
    text-decoration: none
</style>
