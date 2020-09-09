<template>
  <v-card>
    <v-toolbar
      flat
      color="grey lighten-3 black--text"
      dark
    >
      <v-toolbar-title>NewArticle</v-toolbar-title>
    </v-toolbar>

    <v-card-text>
      <v-text-field filled label="Title" v-model="form.title"></v-text-field>

      <v-text-field filled label="img_url" v-model="form.img_url"></v-text-field>

      <v-select
        v-model="form.category_id"
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
        @click="submit"
        color="orange"
        depressed
      >
        Add Post
      </v-btn>
    </v-card-actions>
  </v-card>
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
          value: 3,
      }],
      form: {
        title: '',
        content: '',
        img_url: '',
        category_id: null
      }
    }),
    methods: {
      async submit() {

        await this.$axios.$post('http://localhost:3004/posts', this.form)

        this.$router.push('/')
      }
    }
  }
</script>
