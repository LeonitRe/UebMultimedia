<template>
  <div
    class="container d-flex align-items-center justify-content-center w-100"
    ref="pixiContainer"
  ></div>

  <div class="container d-flex align-items-center justify-content-center">
    <button class="btn btn-primary btn-sm me-5 ms-3" @click="selectCharacter(0)">
      Character 1
    </button>
    <button class="btn btn-primary btn-sm me-5" @click="selectCharacter(1)">Character 2</button>
    <button class="btn btn-primary btn-sm" @click="selectCharacter(2)">Character 3</button>
  </div>
</template>

<script setup>
import * as PIXI from 'pixi.js'
import { onMounted, ref } from 'vue'
import pacman from '../assets/pacman.jpg'
import mario from '../assets/supermario.jpg'
import tetris from '../assets/tetris.jpg'
const characters = [mario, pacman, tetris]

const pixiContainer = ref(null)
const selectedCharacter = ref(0)
let app, sprite, textures

onMounted(() => {
  app = new PIXI.Application({
    width: 1263,
    height: 400,
    backgroundColor: 0x000000
  })

  pixiContainer.value.appendChild(app.view)

  textures = characters.map((character) => PIXI.Texture.from(character))

  sprite = new PIXI.Sprite(textures[selectedCharacter.value])
  sprite.anchor.set(0.5)
  sprite.x = app.view.width / 2
  sprite.y = app.view.height / 2

  app.stage.addChild(sprite)

  let isDragging = false
  let prevMouseX = 0

  app.view.addEventListener('mousedown', onMouseDown)
  app.view.addEventListener('mousemove', onMouseMove)
  app.view.addEventListener('mouseup', onMouseUp)

  function onMouseDown(event) {
    isDragging = true
    prevMouseX = event.clientX
  }

  function onMouseMove(event) {
    if (isDragging) {
      const delta = event.clientX - prevMouseX
      sprite.rotation += delta * 0.01
      prevMouseX = event.clientX
    }
  }

  function onMouseUp() {
    isDragging = false
  }

  app.ticker.add(rotateCharacter)
})

function rotateCharacter() {
  sprite.rotation += 0.01
}

function selectCharacter(index) {
  selectedCharacter.value = index
  sprite.texture = textures[index]
}
</script>
