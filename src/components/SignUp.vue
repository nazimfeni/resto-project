<template>
    <img class="logo" src="../assets/logo.png" alt="" srcset="" >
<h1>Sign Up</h1>
<div class="register">
<input type="text" v-model="name" placeholder="Enter Name" />
<input type="email" v-model="email" placeholder="Enter Email" />
<input type="password" v-model="password" placeholder="Enter Password" />
<button v-on:click="signUp">Sign Up</button>
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
                    alert("Sign Up done")
                }
                // used for saved user info in client browser as localstorage
                localStorage.setItem("user-info",JSON.stringify(result.data))
            }
        }
   

}

</script>

<style>
.logo{
    width: 100px;
}

.register input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.register button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: #fff;
    background-color: skyblue;
    cursor: pointer;
}
</style>