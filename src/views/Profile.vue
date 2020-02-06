<template>
<div>
    <div v-if="!isLogined">
        <v-list-item link
                     to="/">
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon> 


          <v-list-item-content>
            <v-list-item-title class="text-left">На главную</v-list-item-title>
          </v-list-item-content>       
        </v-list-item>
    </div>
    <div>
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    {{user.name}}
                </h1>
            </v-col>
        </v-row>

        <v-row class="text-left">
            <v-col cols="2">
                <img :src="user.photo" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт: <a :href="urlUpgrade(user.website)" target="_blank">{{user.website}}</a>
                </p>
                <p>
                    E-mail: <a :href="`mailto:${user.email}`">{{user.email}}</a>
                </p>
                <p>
                    Город: {{user.city}}
                </p>
                <p>
                    Место работы: {{user.company}}
                </p>
            </v-col>
        </v-row>
        <v-divider class="my-3"></v-divider>
        <v-row class="text-left">
        <v-col cols="9">
            <h2>Сделайте новую публикацию!</h2>
            <v-text-field 
            outlined
            label="Заголовок"
            v-model="name">
            </v-text-field>
            <v-text-field 
            outlined
            label="Текст"
            v-model="text">
            </v-text-field>
        <v-btn color="blue" @click="send()">Опубликовать</v-btn>
        </v-col>
        </v-row>
        
        <v-divider class="my-3"></v-divider>
        <v-row class="text-left">
                <h2>Публикации</h2>
            <v-col cols="9">
                <Post v-for="post in posts"
                      :key="post.id"
                      :title="post.title"
                      :author="user.name"
                      :text="post.body"
                      :img="user.photo"
                      class="post">
                </Post>
            </v-col>
        </v-row>
    </div>
</div>
</template>


<script>
import Post from '../components/Post.vue'

export default {
    props: ['curUserId', 'isLogined', 'axiosLink'],
    components: {
      Post
    },
    data(){
        return {
            posts: [],
            user: {},
            name : '',
            text : ''
        }
    },
    watch: {
        $route: {
            handler(){
                this.upd();
            },
            immediate: true,
        }
    },
    methods: {
        urlUpgrade (url) {
            if (url[0] == 'h')
                return url;
            else
                return 'http://' + url;
        },
        upd () {
            this.$axios.get(this.axiosLink)
                .then(response=>{
                    this.user = response.data[(this.$route.params.id - 1)]
                })
            this.$axios.get('http://jsonplaceholder.typicode.com/posts?userId=' + this.$route.params.id)
                .then(response=>{
                    this.posts = response.data;
            })
        },
        send(){
             this.$axios.get('http://jsonplaceholder.typicode.com/posts')
                .then((responce) => {
                    let curMes = responce.data;
                    this.$axios.post('http://jsonplaceholder.typicode.com/posts/',
                        {'userId': parseInt(this.$route.params.id),
                        'id' : parseInt(curMes[curMes.length - 1].id) + 1,
                        'title' : this.name,
                        'body' : this.text}
                        ).then(()=>{
                            window.alert('Пост опубликован!');
                            this.upd();
                    });
                })
        }
    },
    mounted() {
        this.upd();
    }
}
</script>

<style>
.post {
    margin-top: 60px;
}
</style>