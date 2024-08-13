<template>
    <img class="logo" src="../assets/logo.png" alt="" srcset="" >
<h1>Sign Up</h1>
<div class="register">
<input type="text" v-model="name" placeholder="Enter Name" />
<input type="email" v-model="email" placeholder="Enter Email" />
<input type="password" v-model="password" placeholder="Enter Password" />
<button v-on:click="signUp">Sign Up</button>
<p>
    <router-link to="/login">Login</router-link>
</p>
</div>
</template>

<script>
//Axios is imported for making HTTP requests to the server.
import axios from 'axios';
export default{
    name: 'SignUp',

    data(){
        return{
            name:'',
            email:'',
            password:''
        }
    },
        methods: {
            async signUp(){
                console.warn("Signup", this.name, this.email, this.password)
                let result = await axios.post("http://localhost:3000/users",{
                    name:this.name,
                    email:this.email,
                    password:this.password
                });
                console.warn(result);
                if(result.status==201){
                      // used for saved user info in client browser as localstorage
                localStorage.setItem("user-info",JSON.stringify(result.data))
                // this is for redirect to Home page
                this.$router.push({name:'Home'})
                }
             
            }
        },

        mounted(){
            let user=localStorage.getItem('user-info');
            if(user)
                { this.$router.push({name:'Home'})  }
        }
}



</script>

<style>
</style>