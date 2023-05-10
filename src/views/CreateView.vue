<template>
  <div class="q-pa-md" style="max-width: 300px">
    <q-form @submit="onSubmit" class="q-gutter-md">
      <q-input v-model="fname" label="First Name" />
      <q-input v-model="lname" label="Last Name" />
      <q-input v-model="username" label="Username" />
      <q-input v-model="password" label="Password" />
      <q-input v-model="email" label="Email" />
      <q-input v-model="avatar" label="Avatar" />
      <q-btn label="Submit" type="submit" color="primary" />
    </q-form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import router from "../router";

const fname = ref("");
const lname = ref("");
const username = ref("");
const password = ref("");
const email = ref("");
const avatar = ref("");

const onSubmit = () => {
  var myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");

  var raw = JSON.stringify({
    fname: fname.value,
    lname: lname.value,
    username: username.value,
    password: password.value,
    email: email.value,
    avatar: avatar.value,
  });

  var requestOptions = {
    method: "POST",
    headers: myHeaders,
    body: raw,
    redirect: "follow",
  };

  fetch("https://www.melivecode.com/api/users/create", requestOptions)
    .then((response) => response.json())
    .then((result) => {
      alert(result.message);
      if (result.status === "ok") {
        router.push("/");
      }
    })
    .catch((error) => console.log("error", error));
};
</script>
