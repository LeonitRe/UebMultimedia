<script setup></script>
<template>
  <main>
    <div class="cont vh-100 d-flex flex-row">
      <div class="first w-50">
        <div class="h-100 d-flex align-items-center justify-content-center">
          <img class="h-50 w-50" src="../assets/logo/logo6.png" alt="" />
        </div>
      </div>
      <div class="second w-50 d-flex flex-column">
        <div class="h-25 w-75 d-flex justify-content-evenly text-light align-items-center">
          <router-link to="/" class="button d-flex justify-content-center align-items-center"
            >Home</router-link
          >
          <router-link to="graph" class="button d-flex justify-content-center align-items-center"
            >Graph</router-link
          >
          <router-link to="tour" class="button d-flex justify-content-center align-items-center"
            >360Tour</router-link
          >
        </div>
        <div class="h-75 d-flex flex-column p-5 justify-content-evenly">
          <h1 class="text-primary">Play the Ultimate Game</h1>
          <h4 class="text-primary">
            Experience the thrill of the game like never before at MR. Join now and win big
          </h4>
        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
.cont {
  background-image: url('https://coolhdwall.com/storage/202105/squid-game-mask-soldier-4k-wallpaper-3840x2160.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  font-family: 'Poppins', sans-serif;
}
img {
  animation-name: spin;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-duration: 5s;
}
@keyframes spin {
  0% {
    transform: rotateX(0deg);
  }
  100% {
    transform: rotateX(-360deg);
  }
}
.button {
  background-color: transparent;

  color: #54b3d6;
  font-size: 20px;
  height: 2.5rem;
  width: 6rem;
  border-radius: 10px;
  border: none;
  transition: color 0.3s ease-in-out, box-shadow 0.5s ease-in-out;
  list-style: none;
  text-decoration: none;
}
.button:hover {
  color: #fff;
  box-shadow: inset 200px 0 0 0 #54b3d6;
}
</style>
