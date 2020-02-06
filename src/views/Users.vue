<template>
<div>
    <v-row v-for="n in (users.length / 2)"
           justify="center"
           :key="n"
    >
        <v-col cols="5">
            <ProfileCard :name="users[cardValue(1, n)].name"
                         :id="cardValue(1, n)"
                         :city="users[cardValue(1, n)].city"
                         :img="users[cardValue(1, n)].photo"
            ></ProfileCard>

        </v-col>
        <v-col cols="5">
            <ProfileCard :name="users[cardValue(2, n)].name"
                         :id="cardValue(2, n)"
                         :city="users[cardValue(2, n)].city"
                         :img="users[cardValue(2, n)].photo"
            ></ProfileCard>

        </v-col>
    </v-row>
</div>
</template>


<script>
import ProfileCard from '../components/ProfileCard.vue'

export default {
    components: {
      ProfileCard
    },
    props: ['axiosLink'],
    data(){
        return {
            users: [],
        }
    },
    watch: {
        $route: {
            handler(){
                this.$axios.get(this.axiosLink)
                .then(response=>{
                    this.users = response.data
                })
            },
            immediate: true,
        }
    },
    methods: {
        cardValue(k, n) {
            if (k == 1)
                return n - 1;
            else
                return n - 1 + (this.users.length / 2);
        }
    }
}
</script>

<style>

</style>