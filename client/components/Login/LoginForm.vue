<script setup lang="ts">
import router from "@/router";
import { useUserStore } from "@/stores/user";
import { ref } from "vue";

const email = ref("");
const password = ref("");
const { loginUser, updateSession, isLoggedIn } = useUserStore();

async function login() {
  await loginUser(email.value, password.value);
  void updateSession();
  if (isLoggedIn) {
    void router.push({ name: "Home" });
  }
}
</script>

<template>
  <form class="pure-form pure-form-aligned" @submit.prevent="login">
    <fieldset>
      <div class="entry" style="text-align: center !important">
        <label for="aligned-name">Email</label>
        <input v-model.trim="email" type="email" id="aligned-name" placeholder="Email" required />
      </div>
      <br />
      <div class="entry" style="text-align: center">
        <label for="aligned-password">Password</label>
        <input type="password" v-model.trim="password" id="aligned-password" placeholder="Password" required />
      </div>
      <div>
        <button type="submit" class="pure-button pure-button-primary">Submit</button>
      </div>
    </fieldset>
  </form>
</template>

<style scoped>
.entry {
  text-align: center !important;
  display: inline-block;
  vertical-align: middle;
  width: 10em;
  margin: 0 1em 0 0;
  padding: 10px;
}

button {
  cursor: pointer;
  outline: 0;
  color: black;
  background-color: #fbfbfb;
  border-color: #fbfbfb;
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  text-align: center;
  border: 1px solid transparent;
  padding: 6px 12px;
  margin-top: 20px;
  font-size: 16px;
  border-radius: 0.25rem;
}
</style>
