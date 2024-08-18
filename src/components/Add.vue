<template>
      <Header />
      <h1>Add Restaurant Page</h1> 
      <form class="add">
            <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name" />
            <input type="text" placeholder="Enter Address" v-model="restaurant.address" name="address" />
            <input type="text" placeholder="Enter Contact" v-model="restaurant.contact" name="contact" />
            <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
      </form>     
      </template>
      
      <script>
      import axios from 'axios'
      import Header from './Header.vue'
      
      export default{
            // eslint-disable-next-line vue/multi-word-component-names
            name: 'Add',
            components:{
                  Header
            },

            data(){

                  return {
                        restaurant:{
                              name:'',
                              address:'',
                              contact:''
                        }
                  }
            },
            methods:{
                 async addRestaurant(){
                        
                        const result= await axios.post("http://localhost:3000/restaurant",{
                            name:this.restaurant.name,
                            address:this.restaurant.address,
                            contact:this.restaurant.contact        

                        });
                        console.warn("Result:", result);
                        if(result.status==201){
                      // used for saved user info in client browser as localstorage
                //  localStorage.setItem("user-info",JSON.stringify(result.data))
                // this is for redirect to Home page
                        this.$router.push({name:'Home'})
                }
                  }
            },

            mounted(){
            let user=localStorage.getItem('user-info');
            if(!user)
                { this.$router.push({name:'SignUp'})  }
        }
}
      </script>
      
      
      <style>
      
      </style>