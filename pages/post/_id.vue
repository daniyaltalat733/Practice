<template>
<v-container class="grey lighten-5">
    <v-row v-for="post in posts" :key="post" cols="12" sm="4">
          <h3>{{post.title}}</h3>
          <p>{{post.body}}</p>
    </v-row>
  </v-container>  
</template>

<script>
import axios from 'axios';
export default {
    async asyncData({ error, params }) {
      try{
        const posts = await axios.get(`https://jsonplaceholder.typicode.com/posts/${params.id}`)  
        return { posts };
      }
      catch(err){
        error({ statusCode: 404, message: 'Post not found'})
      }  
 },
 data() {
   return {
     id: this.$route.params.id
   };
 },
 computed: {
   post() {
     return this.posts.find(post => post.id === this.id)
   }
 },
}
</script>>