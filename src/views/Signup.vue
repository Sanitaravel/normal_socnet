<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Регистрация
            </v-card-title>
            
            <div v-for="field in userGaps" :key="field.label">
                <div align="left">{{field.shortLabel}}</div>
                <v-text-field :label="field.label"
                              v-model="userInfo[field.item]"
                              outlined
                              @keyup.enter="signUp"
                ></v-text-field>
            </div>

            <v-btn @click="signUp"
                @keyup.enter="signUp"
                color="success"
            >
                Зарегистрироваться
            </v-btn>
        </v-card>
    </div>
</template>

<script>
export default {
    props: ['axiosLink'],
    data() {
      return {
        userInfo: {
            'login' : '', 
            'password' : '',
            'name' : '',
            'website' : '',
            'email': '',
            'city': '',
            'company' : '',
            'photo' : '',
        },
        userGaps: [
            {
                item: 'login',
                label: 'Введите логин',
                shortLabel: 'Логин',
            },
            {
                item: 'password',
                label: 'Введите пароль',
                shortLabel: 'Пароль',
            },
            {
                item: 'name',
                label: 'Введите имя',
                shortLabel: 'Имя',
            },
            {
                item: 'website',
                label: 'Введите адрес Вашего сайта',
                shortLabel: 'Сайт',
            },
            {
                item: 'email',
                label: 'Введите адрес вашей почты',
                shortLabel: 'Почта',
            },
            {
                item: 'city',
                label: 'Введите город',
                shortLabel: 'Город',
            },
            {
                item: 'company',
                label: 'Введите название компании',
                shortLabel: 'Компания',
            },
            {
                item: 'photo',
                label: 'Введите ссылку на изображение',
                shortLabel: 'Аватарка',
            },
        ],
      }  
    },
    methods: {
        signUp () {
            this.axios.get(this.axiosLink)
                .then((responce) => {
                    let curUsers = responce.data;
                    curUsers[curUsers.length] = {
                        'login' : this.userInfo.login, 
                        'password' : this.userInfo.password,
                        'name' : this.userInfo.name,
                        'website' : this.userInfo.website,
                        'email': this.userInfo.email,
                        'city': this.userInfo.city,
                        'company' : this.userInfo.company,
                        'photo' : this.userInfo.photo,
                    }
                    this.axios.put(this.axiosLink, curUsers);
                    window.alert('Вы успешно зарегистировалтсь! Войдите в аккаунт');
                    this.$router.push('/login');
                })
        },
        reset () {
            for (let i =0;i<this.userInfo.length;i++){
                this.userInfo[i] = ""
            }
        },  
    } 
}
</script>