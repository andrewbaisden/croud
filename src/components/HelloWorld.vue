<template>
  <v-container>
    <v-layout text-xs-center wrap>
      <v-flex mb-5 xs12>
        <h1 class="display-2 font-weight-bold mb-3">Dashboard</h1>
        <h2 class="subheading font-weight-regular">User Data</h2>
      </v-flex>
      <UserList
        :data="data"
        :onUserSelect="onUserSelect"
        :updateUser="updateUser"
        @user="userData.name = $event"
        @email="userData.email = $event"
        @company="userData.company = $event"
      />
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";
import UserList from "./UserList.vue";

const API = "https://jsonplaceholder.typicode.com/users";

export default {
  components: {
    UserList
  },
  data() {
    return {
      data: null,
      selectedUser: null,
      userData: {
        name: "",
        email: "",
        company: ""
      }
    };
  },
  mounted() {
    axios
      .get(API)
      .then(response => {
        console.log("Response", response);
        console.log("Data", response.data);
        this.data = response.data;
      })
      .catch(error => console.log(error));
  },
  methods: {
    updateUser() {
      console.log("Clicked update user button");
      console.log(
        "Users Data for API:",
        this.userData.name,
        this.userData.email,
        this.userData.company
      );
      const formData = {
        name: this.userData.name,
        email: this.userData.email,
        company: {
          name: this.userData.company
        }
      };
      console.log(formData);
      axios
        .put("https://jsonplaceholder.typicode.com/users/1", formData)
        .then(response => {
          console.log("Updated Response on API", response);
          console.log("Updated Data on API", response.data);
        })
        .catch(error => console.log(error));
    },
    onUserSelect(user) {
      console.log("From the App!", user);
      if (user.id) {
        console.log(`Clicked userID:${user.id}`);
        console.log("The users data in the parent", this.userData);
      }
    }
  }
};
</script>

<style>
ul {
  list-style: none;
}
</style>
