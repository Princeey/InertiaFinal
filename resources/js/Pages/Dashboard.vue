<script setup>
import MyLayout from '@/Layouts/MyLayout.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

defineOptions({
  layout: MyLayout
});

const showImage = ref(false);

function toggleImageDisplay() {
  showImage.value = !showImage.value;
}
</script>

<template>
    <div class="py-12 welcome" :style="{ '--primary-color': '#0099cc', '--secondary-color': '#ffffff' }">
      <div class="container">
        <div class="card">
          <div class="card-body">
            <div class="p-12 d-flex justify-content-center">
              <img
                src="../Components/Welcome.jpeg"
                alt="me"
                class="img-fluid welcome-img"
                :class="{ 'fade-in': showImage }"
                @mouseover="toggleImageDisplay"
                @mouseleave="toggleImageDisplay"
                loading="lazy"
                style="width: 50%; height: auto; margin: 0 auto;"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <style scoped>
  .welcome {
    --primary-color: #0099cc; /* A shade of blue */
    --secondary-color: #ffffff; /* White */
    background-color: var(--primary-color);
    color: var(--secondary-color);
    font-family: 'Open Sans', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  
  .welcome-img {
    opacity: 0;
    transition: opacity 0.5s ease-in-out, filter 0.5s ease-in-out;
    filter: grayscale(100%);
  }
  
  .welcome-img:hover {
    filter: grayscale(0);
  }
  
  .fade-in {
    animation: fade-in 1s ease-in-out forwards;
  }
  
  @keyframes fade-in {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  </style>
