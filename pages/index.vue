<template>
  <v-container class="grey lighten-5">
    <v-row>
      <v-col v-for="post in postData" :key="post.title" cols="12" sm="4">
        <nuxt-link :to="{ name: 'post-id' , params: { id:post.id } }" :key="post.id">
        <v-card class="pa-8" outlined tile>
          {{ post.title }}
           </v-card>
        </nuxt-link>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  async asyncData ({error, params}) {
    try{
     const posts = await axios.get(`https://jsonplaceholder.typicode.com/posts`)
     return { postData: posts.data };
    }
  catch (err) {
    error({ statusCode: 404, message: 'Post not found'})
  }
  },
}
</script>
