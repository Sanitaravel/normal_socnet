<template>
  <v-card
    class="mx-auto"
  >
    <v-list-item class="text-left">
      <v-row>
        <v-col cols="2">
            <v-list-item-avatar size="75">
              <img :src="img">
            </v-list-item-avatar>
        </v-col>
        
        <v-divider
          class="mx-3 my-4"
          vertical
        ></v-divider>
        <v-col>
          <v-list-item-content>
            <v-list-item-title class="headline">{{name}}</v-list-item-title>
            <v-list-item-subtitle>{{city}}</v-list-item-subtitle>
          </v-list-item-content>
        </v-col>
      
      </v-row>
    </v-list-item>

    <v-list-item link :to="'/users/' + (id + 1)">
      <i class="mdi mdi-account-box-outline"></i>
      <div class="mx-2">Перейти в профиль</div>
    </v-list-item>

  </v-card>
</template>

<script>
export default {
    props: ['name', 'id', 'city', 'img'],
    data(){
        return {
        }
    }
}
</script>

<style>
.mdi {
  font-size: 20px;
}
</style>
