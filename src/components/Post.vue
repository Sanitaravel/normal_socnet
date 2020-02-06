<template>
  <v-card
    class="mx-auto"
  >
    <v-list-item>
      <v-list-item-avatar>
        <img :src="img">
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title class="headline">{{title}}</v-list-item-title>
        <v-list-item-subtitle>by {{author}}</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-card-text>
      {{text}}
    </v-card-text>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-share-variant</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
</template>


<script>
export default {
    props: ['title', 'author', 'text', 'img'],
    data(){
        return {
        }
    }
}
</script>

<style>
</style>
