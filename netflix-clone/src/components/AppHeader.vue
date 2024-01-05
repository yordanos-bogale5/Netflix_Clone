<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from "vue";
const isDark = ref(false);

const menu = [
  "Home",
  "TV Shows",
  "Movies",
  "Latest",
  "My List",
  "Audio & Subtitles",
];

const changeTheme = () => {
  if (window.scrollY > 100) {
    isDark.value = true;
  } else {
    isDark.value = false;
  }
};

onMounted(() => {
  window.addEventListener("scroll", changeTheme);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", changeTheme);
});
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 px-8 h-16 flex items-center z-30"
    :class="{ 'header-transparent': !isDark, 'bg-black': isDark }"
  >
    <a href="/" class="logo inline-block text-2xl"></a>
    <ul class="m-0 p-0 flex text-xs">
      <li class="ml-4" v-for="item in menu" :key="item">
        <a href="/">{{ item }}</a>
      </li>
    </ul>
  </header>
</template>

<style>
.header-transparent {
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.7) 10%,
    rgba(0, 0, 0, 0)
  );
}

.logo {
  color: #e50914;
  font-family: nf-icon;
}

.logo::before {
  content: "\e5d0";
}
</style>
