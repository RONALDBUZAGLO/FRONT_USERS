<template>
  <div>

      <div class="columns is-mobile is-centered">
        <div class="column is-half">
            <h2>Login</h2>
            <hr>
            <div v-if="error != undefined">
                <div class="notification is-danger is-light">
                    <p>{{error}}</p>
                </div>
                
                
            </div>
            
            <input type="email" placeholder="email@email.com" class="input" v-model="email">     <p>Senha</p>
            <input type="password" placeholder="*******" class="input" v-model="password">
            <button class="button is-success" @click="login">Logar</button>   
        </div>
      </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
    data(){
        return {
            password:"",
            email:"",
            error: undefined,
        }
    },
    methods:{
        login(){
            axios.post("http://localhost:8686/login",{
                password:this.password,
                email:this.email
            }).then(res=>{
                console.log(res);
                localStorage.setItem("token",res.data.token);
                this.$router.push({name:'Home'});
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