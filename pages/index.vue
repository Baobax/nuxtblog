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
        <v-col v-for="post in 4" :key="post" cols="12" md="6">
          <v-card elevation="0">
            <v-card-title>My First Blog</v-card-title>
            <v-card-text
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt
              ratione quam quia eveniet repellendus inventore sint eius possimus
              debitis blanditiis.</v-card-text
            >
            <v-card-actions>
              <v-btn text to="/1">Read More</v-btn>
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
  data: () => ({
    category: 'All',
  }),
}
</script>
