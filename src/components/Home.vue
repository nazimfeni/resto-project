<template>
  <Header />
  <h1>Hello {{ name }} Welcome to Home Page</h1>
  <table border="1">
    <tr>
      <td>ID</td>
      <td>Name</td>
      <td>Address</td>
      <td>Contact</td>
      <td>Action</td>
    </tr>
    <tr v-for="item in restaurants" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td><router-link :to="'/update/' + item.id">Update</router-link></td>
      <button v-on:click="deleteRestaurant(item.id)">Delete</button>
    </tr>
  </table>
</template>

<script>
import axios from "axios";
import Header from "./Header.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Home",
  data() {
    return {
      name: "",
      restaurants: [],
    };
  },
  components: {
    Header,
  },

  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);

      if (result.status == 200) {
        this.loadData();
      }
    },

    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      // eslint-disable-next-line no-unused-vars
      let result = await axios.get("http://localhost:3000/restaurant");
      this.restaurants = result.data;
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style>
td {
  width: 160px;
  height: 40px;
}
</style>
