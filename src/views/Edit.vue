<template>
    <div>
        <h2>Edição de Usuário</h2>
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
                <hr>
                <button class="button is-success" @click="update">Editar</button>
            </div>
        </div>
    </div>    
</template>

<script>
import axios from "axios";
    export  default {
        created(){

            var req = {
                headers:{
                    Authorization: "Bearer " + localStorage.getItem("token")
                }
            }

            axios.get("http://localhost:8686/user/"+this.$route.params.id, req).then((res) => {
                console.log(res)

                this.name = res.data.name;
                this.email = res.data.email;
                this.id = res.data.id
            }).catch((err) => {
                console.log(err.response)
                this.$router.push({name: "Users"})
            })
        },
        data(){
            return {
                name: "",                
                email: "",
                id: -1,
                error: undefined
            }
        }, 
        methods:{            
            update(){
                axios.post("http://localhost:8686/user", {
                    name: this.name,                    
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