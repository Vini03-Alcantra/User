<template>
    <div>
        <h1>Admin Painel</h1>
        <div>            
            <p>Users</p>
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>Nome</th>
                    <th>Email</th>
                    <th>Cargo</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td>{{user.name}}</td>
                    <td>{{user.email}}</td>
                    <td>{{user.role | processRole}}</td>
                    <td>
                        <button class="button is-success">Editar</button> | 
                        <button class="button is-danger" @click="showModalUser(user.id)">Deletar</button>    
                    </td>
                </tr>
            </tbody>
        </table>

        <div :class="{modal: true, 'is-active': showModal}">
            <div class="modal-background"></div>
            <div class="modal-content">
                <div class="card">
                    <header class="card-header">
                        <p class="card-header-title">
                            Você quer realmente deleter esse usuário
                        </p>                        
                    </header>
                    <div class="card-content">
                        <div class="content">
                            <p>Você está prestes a deletar o usuário</p>
                        </div>
                    </div>
                    <footer class="card-footer">                        
                        <a href="#" class="card-footer-item" @click="hideModal()">Fechar</a>
                        <a href="#" class="card-footer-item">Deletar</a>
                    </footer>
                </div>
            </div>
            <button class="modal-close is-large" aria-label="close" @click="hideModal()"></button>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default{
    created(){

        var req = {
            headers:{
                Authorization: "Bearer " + localStorage.getItem("token")
            }
        }
        axios.get("http://localhost:8686/user", req).then(res => {
            console.log(res)
            this.users = res.data
        }).catch((err) => {
            console.log(err)
        })
        console.log("Olá")
    },
    data(){
        return {
            users: [],
            showModal: false
        }
    },
    methods: {
        hideModal(){
            this.showModal = false
        },
        showModalUser(id){
            console.log("Id do user: " +id)
            this.showModal = true
        }
    },
    filters: {
        processRole: function(value){
            if (value == 0) {
                return "Usuário"
            }else if(value == 1){
                return "Admin"
            }
        }
    }
}
</script>

<style scoped>
    
</style>