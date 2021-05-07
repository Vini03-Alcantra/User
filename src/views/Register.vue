<template>
    <div>
        <h2>Registro de Usuário</h2>
        <hr>
        
        <div class="columns is-centered">
            <div class="column is-half">
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
    export  default {
        data(){
            return {
                name: "",
                password: "",
                email: ""
            }
        }, 
        methods:{            
            register(){
                console.log(this.name);
                console.log(this.password);
                console.log(this.email);
            }
        }
    }
</script>

<style scoped>

</style>