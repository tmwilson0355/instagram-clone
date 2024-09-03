<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { useRouter } from 'vue-router';
import UserFeed from './components/UserFeed.vue';

const router = useRouter()

function returnHome() {
  router.push('/')
}

</script>

<template>
  <div class="image-container">
    <img class="header-img" src="/Users/twilson96/Library/CloudStorage/OneDrive-Humana/Desktop/vue-instagram/src/assets/insta.jpeg" @click="returnHome()">
  </div>
  <main>
    <router-view></router-view>
  </main>

</template>

<style scoped>
.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
