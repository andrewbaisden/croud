<template>
  <v-flex mb-5 xs12>
    <ul>
      <li v-for="datas in data" :key="datas.id" @click="onUserSelect(datas)">
        <v-card class="spacing">
          <form @submit.prevent="updateUser">
            <v-card-title>
              <p>{{datas.id}}</p>
            </v-card-title>

            <v-card-text>
              <input v-bind:placeholder="datas.name" id="name" v-model.lazy="userData.name">
            </v-card-text>
            <v-card-text>
              <input v-bind:placeholder="datas.email" id="email" v-model.lazy="userData.email">
            </v-card-text>
            <v-card-text>
              <input
                v-bind:placeholder="datas.company.name"
                id="company"
                v-model.lazy="userData.company"
              >
            </v-card-text>
            <v-card-text>
              <v-btn>
                <button
                  :class="`${datas.id}`"
                  v-on:click="updateUser(); updateState();"
                  type="submit"
                >Update User</button>
              </v-btn>
            </v-card-text>
          </form>
        </v-card>
      </li>
    </ul>
  </v-flex>
</template>

<script>
export default {
  data() {
    return {
      userData: {
        name: "",
        email: "",
        company: ""
      }
    };
  },
  props: ["data", "onUserSelect", "updateUser"],
  methods: {
    updateState() {
      console.log("Updated state");
      this.$emit("user", this.userData.name);
      this.$emit("email", this.userData.email);
      this.$emit("company", this.userData.company);
    }
  }
};
</script>

<style>
.spacing {
  margin-bottom: 1rem;
}
input {
  text-align: center;
  font-size: 1.1rem;
}
</style>
