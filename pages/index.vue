<template>
  <v-row justify="center" align="center">
    <v-overlay :value="overlay">
      <v-progress-circular indeterminate size="70" color="primary"></v-progress-circular>
    </v-overlay>
    <v-col cols="12">
      <h1>MAQE FORUM</h1>
    </v-col>
    <v-col cols="12">
      <p>Your current timezone is: {{timeZone()}}</p>
    </v-col>
    <v-col class="my-2" cols="12" v-for="(post, index) in posts" :key="index">
      <card :post="post" :index="index" :time="timePost(post.created_at)"></card>
    </v-col>
  </v-row>
</template>

<script>
  var moment = require('moment-timezone');
  moment.tz.setDefault("Asia/Bangkok");
  import card from '../components/card.vue'
  export default {
    components: {
      card
    },
    data() {
      return {
        zone: '',
        posts: [],
        overlay: true
      }
    },
    methods: {
      timeZone() {
        let m = moment();
        m.tz();
        return m.tz();
      },
      timePost(time){
        return moment(time).format('LLLL')
      },
      async getAuthors() {
        this.overlay = true;
        await this.$axios.get(
            "https://maqe.github.io/json/authors.json"
          )
          .then(response => {
            let authors = response.data;
            this.getPosts(authors);
          })
          .catch(error => {
            console.log("error", error);
            this.overlay = false;
          })
      },
      async getPosts(authors) {
        this.overlay = true;
        await this.$axios.get(
            "https://maqe.github.io/json/posts.json"
          )
          .then(response => {
            this.posts = response.data;
            this.posts.forEach(p => {
              let result = authors.find(authors => {
                return authors.id === p.author_id
              });
             p["author"] = result;
            })
          this.overlay = false;
          })
          .catch(error => {
            console.log("error", error);
            this.overlay = false;
          })
      }
    },
    mounted() {
      this.getAuthors();
    },
  }
</script>