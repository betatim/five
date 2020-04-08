<template>
  <v-app id="videoIdent">
    <v-content>
      <v-container class="fill-height" fluid>
         <v-layout>
            <script src="https://js.stripe.com/v3/" />
            <v-row align="center" justify="center">
              <v-col cols="12" sm="10" md="6">
                <nuxt />
              </v-col>
            </v-row>
         </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>
