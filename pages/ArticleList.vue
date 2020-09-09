<template>
  <v-container>
    <nuxt-link to="/NewArticle">
      <v-btn>
        新增文章
      </v-btn>
    </nuxt-link>
    <v-row>
      <v-col
        v-for="n in 3"
        :key="n"
        cols="sm"
      >
        <v-card
            class="mx-auto"
            max-width="350"
            color="grey lighten-5"
          >
            <v-img
              class="white--text align-end"
              height="200px"
              src="https://i.imgur.com/kngfqSB.jpg"
            >
              <v-card-title>Post Title</v-card-title>
            </v-img>

            <v-card-subtitle class="pb-0 black--text">Number 10</v-card-subtitle>

            <v-card-text class="grey--text">
              <div>Whitehaven Beach</div>

              <div>Whitsunday Island, Whitsunday Islands</div>
            </v-card-text>

            <v-card-actions>
              <v-btn
                color="orange"
                text
              >
                More
              </v-btn>
            </v-card-actions>
          </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    computed: {
      cols () {
        const { sm } = this.$vuetify.breakpoint
        return sm ? [9, 3] : [6, 6]
      },
    },
  }
</script>
