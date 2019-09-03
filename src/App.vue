<template>
    <Users />
</template>

<script>
import Users from "./components/users.vue";

export default {
  name: "users",
  components: {
    Users
  }
};
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  font-family: "Lato", sans-serif;
  background-color: #eceff1;
  color: #4d4d4d;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
