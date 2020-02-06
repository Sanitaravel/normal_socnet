<template>
  <v-app id="app">
    <div>
    <v-app-bar
      color="blue"
      dense
      dark
    >
      <v-toolbar-title>НеВКтонтакте</v-toolbar-title>
    </v-app-bar>
    <v-navigation-drawer v-if="isLogined"
                           color="blue"
                           dark
                           expand-on-hover
                           hide-overlay
                           right
                           app>
        <v-list nav 
                shaped
                dense>
          <v-list-item two-line>
            <v-list-item-avatar>
              <img :src="currentUser.photo" alt="мужчина">
            </v-list-item-avatar>

            <v-list-item-content class="text-left">
              <v-list-item-title class="font-weight-black">{{currentUser.company}}</v-list-item-title>
              <v-list-item-subtitle>{{currentUser.name}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          

          <v-list-item link
                       v-if="isLogined"
                       @click="logout">
              <v-list-item-icon>
                <v-icon>mdi-logout</v-icon>
              </v-list-item-icon> 

              <v-list-item-content>
                <v-list-item-title class="text-left">Выйти</v-list-item-title>
              </v-list-item-content>
            </v-list-item>

          <!-------------------------------------------->
          <v-divider class="my-3"></v-divider>

          <v-list-item link
                       v-for="link in links" 
                       :key="link.path" 
                       :to="link.path"
                       @click="link.action"
                       exact>
            <v-list-item-icon>
              <v-icon>{{link.icon}}</v-icon>
            </v-list-item-icon> 

            <v-list-item-content>
              <v-list-item-title class="text-left">{{link.label}}</v-list-item-title>
            </v-list-item-content>       
          </v-list-item>
        </v-list>
      </v-navigation-drawer>
    
    <v-content class="px-12 py-3">
      <v-container fluid>
        <router-view v-on:login="updateUser"
                     :isLogined="isLogined"
                     :curUserId="curUserId"
                     :axiosLink="axiosLink"/>
      </v-container>
    </v-content>
  </div>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      links: [
        {
          label: "Главная",
          path: "/",
          icon: "mdi-home-outline",
          action: "",
        },
        {
          label: "Профиль",
          path: "/users/",
          icon: "mdi-account",
          action: "",
        },
        {
          label: "Найти друзей",
          path: "/users",
          icon: "mdi-account-plus",
          action: "",
        },
      ],
      isLogined: false,
      currentUser: {},
      curUserId: '',
      axiosLink: 'http://188.225.47.187/api/jsonstorage/3d54e46db9a9f7b20f72611142687ab5',
    }
  },
  methods: {
    updateUser(_id, user) {
      this.isLogined = true;
      this.curUserId = _id;
      this.currentUser = user;
      this.links[1].path = "/users/" + _id;
    },
    logout() {
      this.isLogined = false;
      this.$router.push('/');
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: blue;
    }
  }
}
</style>
