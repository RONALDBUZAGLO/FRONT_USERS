<template>
  <div>

      <div class="columns is-mobile is-centered">
        <div class="column is-half">
            <h2>Registro de usuário</h2>
            <hr>
            <div v-if="error != undefined">
                <div class="notification is-danger is-light">
                    <p>{{error}}</p>
                </div>
                
                
            </div>
            
            <p>Nome</p>
            <input type="text" placeholder="Nome do Usuário" class="input" v-model="name">  <p>Email</p>
            <input type="email" placeholder="email@email.com" class="input" v-model="email">     <p>Senha</p>
            <input type="password" placeholder="*******" class="input" v-model="password">
            <button class="button is-success" @click="register">Cadastrar</button>   
        </div>
      </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
    data(){
        return {
            name:"",
            password:"",
            email:"",
            error: undefined,
        }
    },
    methods:{
        register(){
            axios.post("http://localhost:8686/user",{
                name:this.name,
                password:this.password,
                email:this.email
                }).then(res=>{
                    this.$router.push({name:'Home'})
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