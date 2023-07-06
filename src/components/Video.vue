<template>
  <div class="background-img d-flex justify-content-center align-items-center flex-column">
    <div class="video-container d-flex justify-content align-items-center w-75 mt-5">
      <video
        class="h-100 w-100"
        ref="videoPlayer"
        :src="currentVideo"
        width="100%"
        height="auto"
      ></video>
    </div>
    <div class="d-flex justify-content-center align-items-center center">
      <div class="btn-group mt-3 me-5">
        <button class="btn btn-primary" @click="playVideo">
          {{ isPlaying ? 'Pause' : 'Play' }}
        </button>
        <button class="btn btn-primary" @click="restartVideo">Restart</button>
        <button class="btn btn-primary" @click="toggleFullScreen">Fullscreen</button>
        <button class="btn btn-primary" @click="toggleMute">
          {{ isMuted ? 'Unmute' : 'Mute' }}
        </button>
      </div>

      <div class="mt-3">
        <h5 class="text-light">Choose a video:</h5>
        <div v-for="(video, index) in videos" :key="index" class="form-check">
          <input
            class="form-check-input"
            type="radio"
            :id="`video${index}`"
            :value="video"
            v-model="currentVideo"
          />
          <label class="form-check-label text-light" :for="`video${index}`">
            Video {{ index + 1 }}
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import marioVideo from '@/components/videos/mario.mp4'
import pacmanVideo from '@/components/videos/pacman.mp4'
import tetrisVideo from '@/components/videos/tetris.mp4'
import { onMounted, ref, watch } from 'vue'

// ...

const videos = ref([marioVideo, pacmanVideo, tetrisVideo])

const currentVideo = ref(videos.value[0])
const isPlaying = ref(false)
const isMuted = ref(false)

const playVideo = () => {
  const video = document.querySelector('video')

  if (video.paused) {
    video.play()
    isPlaying.value = true
  } else {
    video.pause()
    isPlaying.value = false
  }
}

const restartVideo = () => {
  const video = document.querySelector('video')
  video.currentTime = 0
}

const toggleFullScreen = () => {
  const videoContainer = document.querySelector('.video-container')

  if (videoContainer.requestFullscreen) {
    videoContainer.requestFullscreen()
  } else if (videoContainer.webkitRequestFullscreen) {
    videoContainer.webkitRequestFullscreen()
  } else if (videoContainer.msRequestFullscreen) {
    videoContainer.msRequestFullscreen()
  }
}

const toggleMute = () => {
  const video = document.querySelector('video')
  video.muted = !video.muted
  isMuted.value = video.muted
}

onMounted(() => {
  const videoPlayer = document.querySelector('video')

  // Change the video source dynamically
  // Example: currentVideo.value = 'path/to/new/video.mp4';
})
watch(currentVideo, () => {
  isPlaying.value = false // Set isPlaying to false when the video changes
})
</script>

<style scoped>
.video-container {
  height: 75vh;
}
.background-img {
  background-color: rgb(158, 158, 158);
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 120vh;
}
</style>
