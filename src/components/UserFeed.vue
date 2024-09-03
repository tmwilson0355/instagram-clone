<script setup>
import { ref } from 'vue';
const props = defineProps(['post'])
const liked = ref(false)

function likeImage(event) {
    // const body = {"username": props.post.username,"likes":props.post.likes++,"postimage":props.post.postimage ,"caption": props.post.caption,"userimage": props.post.userimage}
    const {post} = props
    liked.value = true
    const body = JSON.stringify({...post, likes: post.likes++})

  let options = {
    
    "method": "PUT",
    "headers": {
        "Accept": "application/json",
        "Content-Type": "application/json"
    },
    body
}
  

  fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post", options)
  .then((response) => {
    return response.json()
  })
  .then(data => {
    props.post = data
  })
}

function unlikeImage() {
    const {post} = props
    liked.value = false
    const body = JSON.stringify({...post, likes: post.likes--})

  let options = {
    
    "method": "PUT",
    "headers": {
        "Accept": "application/json",
        "Content-Type": "application/json"
    },
    body
}
  

  fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post", options)
  .then((response) => {
    return response.json()
  })
  .then(data => {
    props.post = data
  })
}

function likeHandler(event) {
    if(liked) {
        likeImage(event)
    } else {
        unlikeImage(event)
    }
}

</script>

<template>
<div class="post-container">
    <div class="card">
        <div class="post-head">
            <img class="user-image" :src="post.userimage">
            <p class="username">{{ post.username }}</p>
        </div>
        <div class="image-slot">
            <img class="post-image" :src="post.postimage">
        </div>
        <div class="likes">
            <img v-if="liked === false" @click="likeImage()" class="gray" src="/Users/twilson96/Library/CloudStorage/OneDrive-Humana/Desktop/vue-instagram/src/assets/heart-icon-y1k.png">
            <img v-else @click="unlikeImage()" class="normal" src="/Users/twilson96/Library/CloudStorage/OneDrive-Humana/Desktop/vue-instagram/src/assets/heart-icon-y1k.png">
            <p class="likes">{{ post.likes }} Likes</p>
        </div>
        <div class="caption">
        <p><span class="username">{{post.username}}: </span>{{ post.caption }}</p>
        </div>
    </div>
</div>
</template>

<style scoped>
.card {
    /* height: 700px; */
    width: 600px;
    /* border: 1px solid black; */
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 20px;
    margin-bottom: 25px;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.post-head {
    display: flex;
    padding: 5px;
}

.user-image {
    width: 45px;
    height: 45px;
    border-radius: 50%;
    padding-right: 5px;
}

.post-image {
    width: 600px;
}

.likes {
    display: flex;
    margin-left: 5px;
}

.username, .likes {
    font-weight: bold;
}

.normal, .gray {
    height: 20px;
    width: 20px;
    align-self: center;
}

.gray {
    -webkit-filter: grayscale(100%);
    -moz-filter: grayscale(100%);
    -o-filter: grayscale(100%);
    -ms-filter: grayscale(100%);
    filter: grayscale(100%);
}

.caption {
    margin-top: -35px;
    margin-left: 5px;
}

</style>