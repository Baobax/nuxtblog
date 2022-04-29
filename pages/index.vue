<template>
  <div>
    <v-container fluid>
      <div class="intro mt-5 mb-8">
        <h1 class="text-h1">NuxtBlog</h1>
        <h2 class="mt-2">100x Your Nuxt Skills 🚀</h2>
      </div>
      <v-row class="posts-container">
        <v-col cols="12">
          <div class="filter">
            <v-select
              v-model="category"
              style="width: 120px"
              outlined
              dense
              hide-details="auto"
              :items="['All', 'Coding', 'Youtube']"
            />
          </div>
        </v-col>
        <v-col v-for="post in posts" :key="post.slug" cols="12" md="6">
          <v-card elevation="0">
            <v-card-title>{{ post.title }}</v-card-title>
            <v-card-text>
              <nuxt-content :document="{ body: post.excerpt }" />
            </v-card-text>
            <v-card-actions>
              <v-btn text :to="post.path">Read More</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <v-row class="post-pagination">
        <v-col cols="12" class="text-right">
          <v-btn>
            <v-icon small>mdi-arrow-left</v-icon>
            Prev.
          </v-btn>
          <v-btn>
            <v-icon small>mdi-arrow-right</v-icon>
            Next
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  layout: 'DefaultLayout',
  async asyncData({ $content }) {
    const limit = 5
    const page = 1

    const fetchedPosts = await $content()
      .limit(limit)
      .sortBy('createdAt', 'desc')
      .skip((limit - 1) * (page - 1))
      .fetch()
      .catch((error) => {
        error({ statusCode: 404, message: 'Page not found' })
      })

    const nextPage = fetchedPosts.length === limit
    const posts = nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts

    return {
      page,
      limit,
      posts,
      nextPage,
    }
  },
  data: () => ({
    category: 'All',
  }),
  // mounted() {
  //   console.log(this.posts)
  // },
}
</script>
