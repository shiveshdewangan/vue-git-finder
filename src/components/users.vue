<template>
  <div class="container">
    <div class="app">
      <div class="header">Git Finder</div>
      <div class="form">
        <form class="inline-form" @submit.prevent="fetchUser">
          <input v-model="user" id="user" type="text" placeholder="Github User" />
          <button type="submit">Submit</button>
        </form>
      </div>
      <div>
        <span class="error" v-if="errors.input">{{errors.input}}</span>
      </div>
    </div>
    <div v-if="!apiError" class="user-list">
      <div class="pre-message" v-if="this.users.length < 1">Please type a github user to get started</div>
      <div v-else v-bind:key="index" v-for="(u, index) in users">
        <article class="user">
          <h3 class="name">
            <em>{{u.name}}</em>
          </h3>
          <img class="avatar" :src="u.avatar_url" :alt="u.login" />
          <div>
            <strong>Repos</strong>:
            <span>{{u.public_repos}}</span>
          </div>
          <p v-if="u.bio">
            <strong>Bio</strong>
            : {{u.bio}}
          </p>
        </article>
      </div>
    </div>
    <div class="api-error" v-else>{{apiError}}</div>
  </div>
</template>

<script>
import axios from "axios";
import { setTimeout } from "timers";

export default {
  name: "Users",
  data() {
    return {
      user: null,
      users: [],
      errors: {
        input: null
      },
      apiError: null
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

      try {
        const { data } = await axios.get(
          `https://api.github.com/users/${this.user}`
        );
        this.users.push(data);
      } catch (error) {
        this.apiError =
          "Something went wrong. Please try again with a valid ID :)";
        setTimeout(() => {
          this.apiError = "";
        }, 3000);
      }
      this.user = "";
    },
    isInputEmpty() {
      return this.user === null;
    }
  }
};
</script>