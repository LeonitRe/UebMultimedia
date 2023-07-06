<template>
  <main>
    <div class="d-flex flex-column bg-dark test2">
      <div class="gallery-cont h-25">
        <div class="wrapper nine">
          <div>
            <h2 class="p-3">
              <span>G</span>
              <span>A</span>
              <span>L</span>
              <span>L</span>
              <span>E</span>
              <span>R</span>
              <span>Y</span>
            </h2>
          </div>
        </div>
      </div>

      <div class="slide-cont h-100 d-flex flex-row justify-content-center align">
        <div class="h-75 w-25 d-flex justify-content-center align-items-center text-light">
          <div class="parent-element">
            <div class="clipped-element rotate" @click="plusDivs(-1)"></div>
          </div>
        </div>
        <div class="h-75 w-75 test d-flex justify-content-center overflow-hidden">
          <div
            v-for="(slide, index) in slides"
            :key="index"
            :class="['slide ', { active: slide.isActive }]"
          >
            <div class="h-100 w-100 d-flex justify-content-center align-items-center">
              <img :src="slide.image" alt="Slide Image" />
            </div>
          </div>
        </div>
        <div class="h-75 w-25 d-flex justify-content-center align-items-center overflow-hidden">
          <div class="parent-element">
            <div class="clipped-element" @click="plusDivs(1)"></div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { onMounted, ref } from 'vue'

let slideIndex = ref(1)
let slides = ref([])

const images = [
  'https://wallpaperaccess.com/full/765395.jpg',
  'https://c4.wallpaperflare.com/wallpaper/502/710/388/8-bit-super-mario-minimalism-video-games-wallpaper-preview.jpg',
  'https://wallpapers.com/images/featured/w0803uyxw8t0g57m.jpg'
]

function plusDivs(n) {
  showDivs((slideIndex.value += n))
}

function showDivs(n) {
  slideIndex.value = n < 1 ? slides.value.length : n > slides.value.length ? 1 : n

  slides.value.forEach((slide, index) => {
    slide.isActive = index === slideIndex.value - 1
  })
}

onMounted(() => {
  slides.value = images.map((image, index) => ({
    image,
    isActive: index === slideIndex.value - 1
  }))
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cherry+Bomb+One&display=swap');
.parent-element {
  filter: drop-shadow(1.5rem 0 0 rgba(126, 126, 126, 0.8))
    drop-shadow(-1.5rem 0 0 rgba(125, 125, 125, 0.8)) drop-shadow(1.5rem 0 0 rgba(70, 70, 70, 0.8))
    drop-shadow(-1.5rem 0 0 rgba(70, 70, 70, 0.8));
  transition: filter 600ms;
}
.test2 {
  box-shadow: inset 0px 0px 26px 30px rgba(0, 0, 0, 0.75);
  height: 125vh;
  background-image: url('https://cutewallpaper.org/23/abstract-wallpaper-macbook-pro/1240614998.jpg');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
}

.parent-element:hover {
  filter: drop-shadow(0 0 0 rgba(126, 126, 126, 0.8));
}

.clipped-element {
  width: 7rem;
  height: 5rem;
  background-color: white;
  clip-path: polygon(10% 0, 50% 0, 100% 50%, 50% 100%, 10% 100%, 50% 50%);
}
.rotate {
  transform: rotate(180deg);
}

h2 {
  -webkit-background-clip: text;
  font-family: 'Cherry Bomb One', cursive;
}
h2 span {
  font-size: 5rem;
  color: #a00303;
  display: inline-flex;
  animation: rotate 2s infinite;
}
@keyframes rotate {
  0%,
  75% {
    transform: rotateY(360deg);
  }
}
.nine span:nth-of-type(1) {
  animation-delay: 0.2s;
}
.nine span:nth-of-type(2) {
  animation-delay: 0.4s;
}
.nine span:nth-of-type(3) {
  animation-delay: 0.6s;
}
.nine span:nth-of-type(4) {
  animation-delay: 0.8s;
}
.nine span:nth-of-type(5) {
  animation-delay: 1s;
}
.nine span:nth-of-type(6) {
  animation-delay: 1.2s;
}
.nine span:nth-of-type(7) {
  animation-delay: 1.4s;
}

img {
  width: 90%;
  height: 85%;
  box-shadow: rgba(240, 46, 170, 0.4) -5px 5px, rgba(240, 46, 170, 0.3) -10px 10px,
    rgba(240, 46, 170, 0.2) -15px 15px, rgba(240, 46, 170, 0.1) -20px 20px,
    rgba(240, 46, 170, 0.05) -25px 25px;
}

.slide {
  display: none;
  flex-shrink: 0;
  width: 100%;
  height: 100%;
}

.slide.active {
  display: block;
}
</style>
