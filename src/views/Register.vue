<template>
    <div>
        <h2>Registro de Usuário</h2>
        <hr>
        
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="error != undefined">                    
                    <div class="notification is-danger">                        
                        <p>{{error}}</p>
                    </div>                    
                </div>
                <p>Name</p>
                <input type="text" placeholder="Name of user" class="input" v-model="name">
                <p>E-mail</p>
                <input type="email" placeholder="email@example.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" placeholder="******" class="input" v-model="password">
                <hr>
                <button class="button is-success" @click="register">Cadastrar</button>
            </div>
        </div>
    </div>    
</template>

<script>
import axios from "axios";
    export  default {
        data(){
            return {
                name: "",
                password: "",
                email: "",
                error: undefined
            }
        }, 
        methods:{            
            register(){
                axios.post("http://localhost:8686/user", {
                    name: this.name,
                    password: this.password,
                    email: this.email
                }).then(() => {
                    this.$router.push({name: "Home"})
                }).catch(err => {
                    var msgError = err.response.data.err
                    this.error = msgError
                })
            }
        }
    }
</script>

<style scoped>

</style>