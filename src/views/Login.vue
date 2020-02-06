<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Войдите в аккаунт
            </v-card-title>

            <v-text-field
                label="Введите логин"
                v-model="login"
                outlined
                @keyup.enter="auth"
            ></v-text-field>

            <v-text-field
                label="Введите пароль"
                :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                :type="show ? 'text' : 'password'"
                name="input-10-2"
                @click:append="show = !show"
                @keyup.enter="auth"
                outlined
                v-model="password"
            ></v-text-field>

            <v-btn @click="auth"
                   @keyup.enter="auth"
                   
            >
                Войти
            </v-btn>
        </v-card>
    </div>
</template>

<script>
export default {
    props: ['axiosLink'],
    data() {
      return {
          password: '',
          login: '',
          show: false,
          rules: {
        },
      }  
    },
    methods: {
        auth() {
            this.axios.get(this.axiosLink)
                .then((responce) => {
                    let users =  responce.data;
                    let found = false;
                    for (let index in users) {
                        if (this.login == users[index].login && this.password == users[index].password) {
                            let id = parseInt(index) + 1;
                            this.$emit('login', id, users[index]);
                            this.$router.push('/users/' + id);
                            found = true;
                            break;
                        }
                    }

                    if (!found) {
                        window.alert('Неверный логин или пароль!');
                    }
                })
        }
    } 
}
</script>