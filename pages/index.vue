<template>
  <div>
    <v-container>
    <nuxt-link to="/NewArticle">
      <v-btn>
        新增文章
      </v-btn>
    </nuxt-link>
    <v-row>
      <v-col
        v-for="post in posts"
        :key="post.id"
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
              :src="post.img_url"
            >
              <v-card-title>{{ post.title }}</v-card-title>
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
              <v-btn depressed small
              class="grey--text"
              color="grey lighten-3"
              to="/EditArticle">
              編輯
              </v-btn>
              <v-btn depressed small
              class="grey--text"
              color="grey lighten-3"
              @click="deletePost"
              >刪除

              </v-btn>
            </v-card-actions>
          </v-card>
      </v-col>
    </v-row>
  </v-container>
  </div>
</template>



<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  },

  async asyncData({ $axios }) {

    const data = await $axios.$get('http://localhost:3004/posts')

    return {
      posts: data
    }
  },

  methods:{
    async deletePost({id}) {
    const ddd = await $axios.$delete(`http://localhost:3004/posts/${id}`,{data: { post }})
    },
  }


  // methods: {
  //   DeleteArticle () {
  //          this.post.splice(this.post.id, 1)

  // const index = this.posts.findIndex(item => item.id === post.id)
  // this.posts.splice(index, 1)
  //       }
  // }




  // async mounted() {
  //   const data = await this.$axios.$get('http://localhost:3004/posts')
  //   this.posts = data
  // }

}
</script>
