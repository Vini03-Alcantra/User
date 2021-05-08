<template>
    <div>
        <hr>

        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="error != undefined">
                    <div class="notification is-danger">
                        <p>{{error}}</p>
                    </div>
                </div>
                <p>Email</p>
                <input type="email" placeholder="email@example.com.br" class="input" v-model="email">
                <p>Password</p>
                <input type="password" placeholder="********" class="input" v-model="password">
                <hr>
                <button class="button is-success" @click="login">Login</button>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {            
            password: "",
            email: "",
            error: undefined
        }
    },
    methods:{
        login(){
            console.log("Login")
        }
    }
}

</script>
