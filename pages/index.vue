<template>
  <div>
    <v-container>
      <ul>
        <li v-for="category in categories" :key="category.value">
          <nuxt-link :to="`/?category=${category.value}`">{{ category.text }}</nuxt-link>
        </li>
      </ul>
    <nuxt-link to="/NewArticle">
      <v-btn>
        新增文章
      </v-btn>
    </nuxt-link>
     <nuxt-link to="/NewArticle">
      <v-btn>
        新增分類
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
              :to="`/EditArticle/${post.id}`">
              編輯
              </v-btn>
              <v-btn depressed small
              class="grey--text"
              color="grey lighten-3"
              @click="deletePost(post.id)"
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

export default {
  async asyncData({ $axios }) {

    const data = await $axios.$get('http://localhost:3004/posts')
    const categories = await $axios.$get('http://localhost:3004/categories')

    categories.push({ value: 'all', text: '所有文章'})

    return {
      posts: data,
      categories
    }
  },
  watch: {
    async $route(val) {
      const category = val.query.category
      let data = []
      if (category === 'all') {
        data = await this.$axios.$get('http://localhost:3004/posts')
      } else {
        data = await this.$axios.$get(`http://localhost:3004/categories/${category}/posts`)
      }
      this.posts = data
    }
  },

  methods:{

    async deletePost(id) {
      console.log(id)

      try{
        await this.$axios.$delete(`http://localhost:3004/posts/${id}`)
        const data = await this.$axios.$get('http://localhost:3004/posts')
        console.log(data)
        this.posts = data
      } catch(e) {
        console.log(e);
      }
    },
  }

//  const data = await $axios.$delete(`http://localhost:3004/posts/${id}`)




  // async mounted() {
  //   const data = await this.$axios.$get('http://localhost:3004/posts')
  //   this.posts = data
  // }

}
</script>
