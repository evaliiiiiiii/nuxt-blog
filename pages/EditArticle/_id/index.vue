<template>
<div>

  <v-card>
    <v-toolbar
      flat
      color="grey lighten-3 black--text"
      dark
    >
      <v-toolbar-title>EditArticle</v-toolbar-title>
    </v-toolbar>

    <v-card-text>
      <v-text-field filled label="Title" v-model="form.title"></v-text-field>

      <v-select
        v-model="form.categoryId"
        :items="categories"
        label="Standard"
      ></v-select>

      <v-textarea
        v-model="form.content"
        filled
        label="Text"
      ></v-textarea>
    </v-card-text>

    <v-divider></v-divider>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        @click="edit"
        color="orange"
        depressed
      >
        Edit Post
      </v-btn>
    </v-card-actions>
  </v-card>
  </div>
</template>

<script>
  export default {
    data: () => ({
      categories: [
      {
          text: '分類1',
          value: 1,
      },
      {
          text: '分類2',
          value: 2,
      },
      {
          text: '分類3',
          value: 3
      }],
      // form: {
      //   title: '',
      //   content: '',
      //   img_url: '',
      //   categoryId: null
      // }
    }),


    async asyncData({ $axios, params }) {

    const data = await $axios.$get(`http://localhost:3004/posts/${params.id}`)
    // console.log($router.params.id)

    return {
        form: data
      }
    },

    methods: {
      async edit() {
        await this.$axios.$patch(`http://localhost:3004/posts/${this.$route.params.id}`, this.form)

        this.$router.push('/')
      },
    }
  }
</script>
