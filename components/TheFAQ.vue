<template>
  <v-container class="px-6 px-md-4">
    <v-row justify="center">
      <v-col cols="12" sm="10" md="11" lg="9" xl="6">
        <div class="faq py-2 py-md-12 my-2 my-md-12">
          <h2
            :class="{ 'text-center': $vuetify.breakpoint.smAndUp }"
            class="display-3 mb-6"
          >
            {{ $t('faq.title') }}
          </h2>
          <v-expansion-panels accordion flat multiple class="my-10">
            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question1.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <div
                  class="v-expansion-panel-content__wrap"
                  v-html="$t('faq.question1.answer')"
                ></div>
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question2.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <div
                  class="v-expansion-panel-content__wrap"
                  v-html="$t('faq.question2.answer')"
                ></div>
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question3.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <p v-html="linkifySkribble($t('faq.question3.answer'))"></p>
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question4.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                {{ $t('faq.question4.answer') }}
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question5.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <i18n
                  path="faq.question5.answer"
                  tag="p"
                  for="faq.question5.answer_linkText"
                >
                  <a
                    class="link"
                    :href="$t('faq.question5.answer_linkURL')"
                    target="_blank"
                    >{{ $t('faq.question5.answer_linkText') }}</a
                  >
                </i18n>
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question7.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <p v-html="linkifySkribble($t('faq.question7.answer'))"></p>
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question8.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                {{ $t('faq.question8.answer') }}
              </v-expansion-panel-content>
            </v-expansion-panel>

            <v-expansion-panel>
              <v-expansion-panel-header>
                {{ $t('faq.question9.question') }}
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                {{ $t('faq.question9.answer') }}
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
export default {
  name: 'TheFAQ',
  methods: {
    // Turns Skribble string into a link pointing to Skribble.com
    linkifySkribble(text: string): string {
      // TODO: replace with lokalised skribble page
      const skribbleHTMLLinkTag = text.replace(
        'Skribble',
        // @ts-ignore
        `<a class="link" href="${this.$t(
          'global.skribbleURL'
        )}" target="_blank">Skribble</a>`
      )
      return skribbleHTMLLinkTag
    },
  },
}
</script>

<style lang="sass">
@import ~/assets/sass/_vars
@import ~/assets/sass/_mixins

.faq
  .theme--light.v-expansion-panels .v-expansion-panel
    color: $c-text

  .v-expansion-panel
    border-bottom: 1px solid $c-border
    &:first-child
      border-top: 1px solid $c-border

    &-header
      padding: 16px 0 16px 0
      font: bold 1rem/1.4 $averta
      color: $c-skribbleu
      +media(xs-only)
        font-size: .9rem

      &__icon
        padding-left: 20px

    &-content__wrap
      padding-left: 0
</style>
