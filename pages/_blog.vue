<template>
  <v-container fluid>
    <section class="my-3 text-right">
      <v-btn text to="/">
        <v-icon small class="mr-2">mdi-arrow-left</v-icon>
        Go Back
      </v-btn>
    </section>
    <section class="post-content">
      <h2 class="text-h2 mb-10">{{ post.title }}</h2>
      <nuxt-content :document="post" />
    </section>
    <v-row>
      <v-col class="d-flex justify-space-between align-center mt-5" cols="12">
        <v-btn :disabled="!prev" :to="prev && prev.path">Prev. Post</v-btn>
        <v-btn :disabled="!next" :to="next && next.path">Next Post</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: 'PostPage',
  layout: 'DefaultLayout',
  async asyncData({ $content, error, params }) {
    // TODO > Paginate

    const [prev, next] = await $content()
      .only(['path'])
      .sortBy('createdAt', 'desc')
      .surround(params.blog)
      .fetch()

    // fetch and render single post:
    const post = await $content(params.blog)
      .fetch()
      .catch(() =>
        error({
          statusCode: 404,
          message: 'Oops, looks like that post does not exist...',
        })
      )

    return {
      post,
      prev,
      next,
    }
  },
}
</script>
<style></style>
