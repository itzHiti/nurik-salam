<template>
  <div id="app">
    <transition name="fade" mode="out-in">
      <div v-if="showLoading" key="loading" class="loading-screen">
        <img alt="Logo" class="logo" src="@/assets/logo.png" />
      </div>
      <div v-else key="content">
        <header>
          <img alt="Logo" class="logo" src="@/assets/logo.png" />
        </header>
        <main>
          <Main />
        </main>
        <footer>
          <button @click="openLink('https://www.tiktok.com/@mementomor32')">TikTok</button>
          <button @click="openLink('https://t.me/dosstar_tiktok')">Telegram</button>
          <button @click="openLink('https://www.instagram.com/dosstar_agency/')">Instagram</button>
          <button @click="openLink('https://wa.me/77714226265')">WhatsApp 1</button>
          <button @click="openLink('https://wa.me/77755666704')">WhatsApp 2</button>
        </footer>
      </div>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Main from './views/Main.vue';

const showLoading = ref(true);;

function openLink(url: string) {
  window.open(url, '_blank');
}

onMounted(() => {
  if (localStorage.getItem('visited')) {
    showLoading.value = false;
  } else {
    setTimeout(() => {
      showLoading.value = false;
      localStorage.setItem('visited', 'true');
    }, 2000);
  }
});
</script>

<style scoped>
#app {
  text-align: center;
}

.loading-screen {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.logo {
  width: 250px;
  height: 250px;
  display: block;
  margin: 0 auto;
  justify-content: center;
}

header,
footer {
  margin: 20px 0;
}

footer {
  display: flex;
  flex-direction: column;
  align-items: center;
}

footer button {
  margin: 5px;
  padding: 12px 24px;
  background: #00f2fe;
  border: none;
  font-family: 'Montserrat', sans-serif;
  font-size: 2em;
  color: #fff;
  cursor: pointer;
  border-radius: 50px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

footer button:hover {
  background: linear-gradient(#00f2fe, #4facfe);
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.2);
  transform: translateY(-3px);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>