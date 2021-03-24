<template>
  <div>

      <div class="columns is-mobile is-centered">
        <div class="column is-half">
            <h2>Edição de usuário</h2>
            <hr>
            <div v-if="error != undefined">
                <div class="notification is-danger is-light">
                    <p>{{error}}</p>
                </div>
                
                
            </div>
            
            <p>Nome</p>
            <input type="text" placeholder="Nome do Usuário" class="input" v-model="name">  <p>Email</p>
            <input type="email" placeholder="email@email.com" class="input" v-model="email">     <p>Senha</p>
            <button class="button is-success" @click="update">Editar</button>   
        </div>
      </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
    created(){
        var req = {
            headers:{
                Authorization: "Bearer "+localStorage.getItem('token')
            }
        }
        axios.get("http://localhost:8686/user/"+this.$route.params.id,req).then(res=>{
            console.log(res);

            this.name = res.data.name;
            this.email = res.data.email;
            this.id = res.data.id
        }).catch(err=>{
            console.log(err);
            this.$router.push({name:'Users'});
        })
    },
    data(){
        return {
            name:"",
            email:"",
            error: undefined,
        }
    },
    methods:{
        update(){

            var req = {
                headers:{
                    Authorization: "Bearer "+localStorage.getItem('token')
                }
            }

            axios.put("http://localhost:8686/user",{
                name:this.name,
                email:this.email,
                id:this.id,
            },req).then(res=>{
                    this.$router.push({name:'Users'})
                console.log(res);
            }).catch(err=>{
                var msgErro = err.response.data.err;
                this.error = msgErro;
                console.log(msgErro);
            });
            // console.log(this.name);
            // console.log(this.password);
            // console.log(this.email);
        }
    }
    

}
</script>

<style scoped>

</style>