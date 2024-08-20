<template>
  <Header />
  <h1>Update Restaurant Page</h1>
  <form class="add">
    <input
      type="text"
      placeholder="Enter Name"
      v-model="restaurant.name"
      name="name"
    />
    <input
      type="text"
      placeholder="Enter Address"
      v-model="restaurant.address"
      name="address"
    />
    <input
      type="text"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
      name="contact"
    />
    <button type="button" v-on:click="updateRestaurant">
      Update Restaurant
    </button>
  </form>
</template>

<script>
import axios from "axios";
import Header from "./Header.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Update",
  components: {
    Header,
  },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },

  methods: {
    async updateRestaurant() {
      const result = await axios.put(
        "http://localhost:3000/restaurant/" + this.$route.params.id,
        {
          name: this.restaurant.name,
          address: this.restaurant.address,
          contact: this.restaurant.contact,
        }
      );
      console.warn("Result:", result);
      if (result.status == 200) {
        // used for saved user info in client browser as localstorage
        //  localStorage.setItem("user-info",JSON.stringify(result.data))
        // this is for redirect to Home page
        this.$router.push({ name: "Home" });
      }
    },
  },

  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get(
      "http://localhost:3000/restaurant/" + this.$route.params.id
    );

    this.restaurant = result.data;
  },
};
</script>

<style></style>
