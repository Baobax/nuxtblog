<template>
  <v-app>
    <!-- Navigation -->
    <TheNavigation />
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12" md="10">
            <Nuxt />
          </v-col>
          <v-col cols="12" md="2">
            <!-- Ads/side content -->
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TheNavigation from '~/components/TheNavigation.vue'
export default {
  name: 'DefaultLayout',
  components: { TheNavigation },
}
</script>

<style></style>
