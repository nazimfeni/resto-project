<template>
      <h1>Welcome to Home Page</h1>      
      </template>
      
      <script>
      export default{
            // eslint-disable-next-line vue/multi-word-component-names
            name: 'Home',

            mounted(){
            let user=localStorage.getItem('user-info');
            if(!user)
                { this.$router.push({name:'SignUp'})  }
        }
}
      </script>
      
      
      <style>
      
      </style>