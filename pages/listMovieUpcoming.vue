<template>
  <div>
    <v-container>
      <v-flex xs4 pb-5>
        <h2>List Upcoming Movie</h2>
      </v-flex>

      <v-flex
        v-for="(result, index) in results"
        :key="index"
        mb-15
        xs4
        style="display: inline-block"
      >
        <v-card class="mx-auto mr-16" max-width="300">
          <img
            :src="'http://image.tmdb.org/t/p/w500' + result.poster_path"
            width="100%"
          />
          <v-card-title class="overflow-auto" style="height: 100px">
            {{ result.title }}</v-card-title
          >
          <v-card-subtitle> {{ result.popularity }}</v-card-subtitle>

          <v-card-actions class="ml-2">
            <v-btn color="orange lighten-2" @click="show = !show">
              Read More
            </v-btn>

            <v-spacer></v-spacer>
            <v-btn icon @click="show = !show">
              <v-icon>{{
                show ? 'mdi-chevron-up' : 'mdi-chevron-down'
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>

              <v-card-text class="overflow-auto" style="height: 100px">
                {{ result.overview }}
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
      </v-flex>
    </v-container>
  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    const { results } = await app.$axios.$get(
      'https://api.themoviedb.org/3/movie/upcoming?api_key=9e752dcafe8ff9dce9317755617f685a&language=en-US&page=1'
    )
    return { results }
  },
  data: () => ({
    show: false,
  }),
}
</script>
