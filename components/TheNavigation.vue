<template>
  <v-app-bar v-if="$route.name === 'index'" max-height="64">
    <div class="search d-flex align-center justify-end ml-auto">
      <v-text-field
        v-model="search"
        hide-details="auto"
        dense
        placeholder="Search for a post"
        prepend-icon="mdi-magnify"
        outlined
        :append-icon="search.length ? 'mdi-close' : ''"
        @click:append="clearSearch"
      />
    </div>
  </v-app-bar>
</template>
<script>
export default {
  name: 'TheNavigation',
  // data: () => ({
  //   search: '',
  // }),
  //  replace:
  computed: {
    search: {
      get() {
        return this.$store.state.query
      },
      set(value) {
        this.$store.commit('SET_QUERY', value)
      },
    },
  },
  methods: {
    clearSearch() {
      // this.search = ''
      this.$store.commit('SET_QUERY', '')
    },
  },
}
</script>
<style></style>
