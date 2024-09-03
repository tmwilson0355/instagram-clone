<script setup>
import router from '@/router';
import { ref } from 'vue';

let username = ref('')
let userImage = ref('')
let imageLink = ref('')
let likes = ref('')
let caption = ref('')

function addNewPost() {
    let options = {
    method: "POST",
    body: JSON.stringify({
      username : username.value,
      userimage: userImage.value,
      postimage: imageLink.value,
      likes: likes.value,
      caption: caption.value
    }),
    headers: {
      Accept: "application/json",
      "Content-Type": "application/json"
    }
  }

  fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post", options)
  .then((response) => {
    return response.json()
  })
  .then(data => {
    router.push('/')
  })
}

</script>

<template>
<div class="newPostForm">
    <label for="username">Username:</label>
    <input type="text" id="username" v-model="username">
    <label for="user-image">User Image:</label>
    <input type="text" id="user-image" v-model="userImage">
    <label for="image-link">Image Link:</label>
    <input type="text" id="image-link" v-model="imageLink">
    <label for="likes">Likes:</label>
    <input type="text" id="likes" v-model="likes">
    <label for="caption">Caption:</label>
    <input type="text" id="caption" v-model="caption">
    <button class="submitBtn" @click="addNewPost()">Submit</button>
</div>
</template>

<style scoped>
.newPostForm {
    display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
}

input, label {
    margin-bottom: 15px;
}

.submitBtn {
    background-color: #0095ff;
  border: 1px solid transparent;
  border-radius: 3px;
  box-shadow: rgba(255, 255, 255, .4) 0 1px 0 0 inset;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-family: -apple-system,system-ui,"Segoe UI","Liberation Sans",sans-serif;
  font-size: 13px;
  font-weight: 400;
  line-height: 1.15385;
  margin: 0;
  outline: none;
  padding: 8px .8em;
  position: relative;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: baseline;
  white-space: nowrap;
}

</style>