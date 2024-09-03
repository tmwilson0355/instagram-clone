<script setup>
import { useRouter } from 'vue-router';
import { ref,reactive } from 'vue';
import UserFeed from '@/components/UserFeed.vue';

const router = useRouter()

function goToNewPostPage() {
  router.push('/newpost')
}

let instaFeed = ref([])
const likes = ref({})
fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post")
.then((response) => {
    return response.json()
}).then((content) => {
    console.log(content)
    instaFeed.value = content
})
</script>

<template>
    <div class="button-container">
    <button class="newPostBtn" @click="goToNewPostPage()">New Post</button>
    </div>
    <div class="image-container">
    <UserFeed v-for="post in instaFeed" :post = "post"></UserFeed>
</div>
</template>

<style scoped>

/* grabbed button styling from css scan */
.newPostBtn {
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

.button-container {
    display: flex;
    justify-content: end;
}

.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
