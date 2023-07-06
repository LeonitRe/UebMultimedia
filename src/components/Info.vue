<template>
  <div class="conts d-flex flex-column align-items-center justify-content-around">
    <div class="word w-100 text-primary p-5" ref="wordRef">Why {{ part }} Game</div>
    <Image1>
      <template #image>
        <h2 class="mario-title">MARIO</h2>
      </template>
      <template #title> MARIO </template>
      <template #description>
        Super Mario Bros. is a platform game. In the game, Mario must race through the Mushroom
        Kingdom and save Princess Toadstool (later Princess Peach) from Bowser. Mario jumps, runs,
        and walks across each level. The worlds are full of enemies and platforms, and open
        holes.</template
      >
    </Image1>
    <Image1>
      <template #image>
        <h2 class="pacman-title">PACMAN</h2>
      </template>
      <template #title> PACMAN </template>
      <template #description>
        Pac-Man is an action maze chase video game; the player controls the eponymous character
        through an enclosed maze. The objective of the game is to eat all of the dots placed in the
        maze while avoiding four colored ghosts — Blinky (red), Pinky (pink), Inky (cyan), and Clyde
        (orange) — that pursue Pac-Man.
      </template>
    </Image1>
    <Image1>
      <template #image>
        <h2 class="tetris-title">TETRIS</h2>
      </template>
      <template #title> TETRIS </template>
      <template #description>
        Tetris is a puzzle game, developed in the Soviet Union in 1985. The game has a simple goal
        of destroying lines of blocks before it reaches the top. The line is made up of a square
        block. The Tetrimino is the shape of the 4 connected blocks that fall down.
      </template>
    </Image1>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Image1 from './Image1.vue'

const words = ['Mario', 'Pacman', 'Tetris']

let part = ref('')
let i = ref(0)
let offset = ref(0)
const len = words.length
let forwards = ref(true)
let skipCount = ref(0)
const skipDelay = 15
const speed = 100

const wordFlick = () => {
  setInterval(() => {
    if (forwards.value) {
      if (offset.value >= words[i.value].length) {
        skipCount.value++
        if (skipCount.value === skipDelay) {
          forwards.value = false
          skipCount.value = 0
        }
      }
    } else {
      if (offset.value === 0) {
        forwards.value = true
        i.value++
        offset.value = 0
        if (i.value >= len) {
          i.value = 0
        }
      }
    }
    part.value = words[i.value].substr(0, offset.value)
    if (skipCount.value === 0) {
      if (forwards.value) {
        offset.value++
      } else {
        offset.value--
      }
    }
  }, speed)
}

onMounted(() => {
  wordFlick()
})
</script>

<style scoped>
@import url('https://fonts.cdnfonts.com/css/public-pixel');
@import url('https://fonts.googleapis.com/css2?family=Cherry+Bomb+One&display=swap');
@import url(https://fonts.googleapis.com/css?family=Saira+Stencil+One);
.word {
  margin-top: 0;
  color: white;
  font: 700 normal 2.5em 'tahoma';
  font-family: 'Public Pixel', sans-serif;
  text-shadow: 5px 2px #222324, 2px 4px #222324, 3px 5px #222324;
}
.conts {
  height: 220vh;
  background-image: url('https://4kwallpapers.com/images/wallpapers/apple-pro-display-xdr-stock-5k-4480x2520-2303.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

h2 {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  margin: 0;
  font-weight: 400;
  font-size: 16vw;
  text-transform: uppercase;
  color: white;

  font-family: 'Saira Stencil One', cursive;
}
.mario-title {
  background-image: url('https://wallpapers.com/images/featured/vbep44x7ca67u2vn.jpg');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
}
.pacman-title {
  background-image: url('https://wallpaperset.com/w/full/5/d/0/55043.jpg');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
}
.tetris-title {
  background-image: url('https://rare-gallery.com/mocahbig/35381-Tetris-HD-Wallpaper.jpg');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover;
}
</style>
