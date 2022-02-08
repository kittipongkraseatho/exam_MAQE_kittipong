<template>
  <v-card>
    <v-card-title class="headline">
      <v-row>
        <v-avatar class="mb-3" size="36px">
          <img alt="Avatar" :src="post.author.avatar_url">
        </v-avatar>
        <p class="pl-3 red--text text-h6">{{post.author.name}}</p>
        <p class="text-h6 pl-3">
          post on {{time}}
        </p>
      </v-row>
    </v-card-title>
    <hr class="my-0 mt-n3">
      <v-row class="pa-3 pb-0">
        <v-col cols="3">
          <v-card class="mx-auto">
            <v-img class="white--text align-end" height="200px" :src="post.image_url">
            </v-img>
          </v-card>
        </v-col>
        <v-col cols="9">
          <v-card-title>
            {{post.title}}
          </v-card-title>

          <v-card-subtitle>
            {{post.body}}
          </v-card-subtitle>
        </v-col>
      </v-row>

  </v-card>
</template>

<script>
  export default {
    props: ["post", "index", "time"],
    data() {
      return {

      }
    },
  }
</script>