<template>
  <div id="app">
    <div>
      <div class="header">Git Finder</div>
      <div class="form">
        <form class="inline-form" @submit.prevent="fetchUser">
          <input v-model="user" id="user" type="text" placeholder="Github User" />
          <button type="submit">Submit</button>
        </form>
      </div>
      <div>
        <span v-if="errors.input">{{errors.input}}</span>
      </div>
    </div>
    <div>
      <div v-if="this.users.length < 1">Please type a github user to get started</div>
      <div v-else v-bind:key="index" v-for="(u, index) in users">
        <strong class="user">
          <h3 :class="name">
            <em>{{u.login}}</em>
          </h3>
          <img :class="avatar" :src="u.avatar_url" :alt="u.login" />
          <div>
            <strong>{{u.public_repos}}</strong>
          </div>
        </strong>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Users",
  data() {
    return {
      user: null,
      users: [],
      errors: {
        input: null
      }
    };
  },
  methods: {
    async fetchUser() {
      if (this.isInputEmpty()) {
        this.errors.input = "Input Field can not be empty";
        this.user = null;
        return;
      }

      this.errors.input = null;

      const { data } = await axios.get(
        `https://api.github.com/users/${this.user}`
      );
      console.log(data);
      this.users.push(data);
      console.log("this.users", this.users);
      this.user = "";
    },
    isInputEmpty() {
      return this.user === null;
    }
  }
};
</script>

<style scoped>
.inline-form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.inline-form input {
  flex: 4;
  padding: 12px 20px;
  margin: 4px;
  box-sizing: border-box;
  border: 2px solid royalblue;
  border-radius: 4px;
}

.inline-form button {
  flex: 1;
  background-color: #3498db;
  border: none;
  color: white;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 4px;
  padding: 10px 20px;
}

.form-inline button:hover {
  background-color: royalblue;
}

input[type="text"]:focus {
  background-color: fff;
}

input::placeholder {
  text-align: center;
}

.user {
  width: 300px;
  padding: 10px;
  margin: 1rem;
  box-shadow: 7px 10px 12px -5px rgba(0, 0, 0, 0.56);
  text-align: center;
  background-color: white;
  border-radius: 5px;
  font-size: 80%;
}

.avatar {
  width: 40%;
  border-radius: 50%;
  box-shadow: 2px 2px 2px -1px rgba(0, 0, 0, 0.56);
}

.user-list {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

.hidden {
  display: none;
}
</style>