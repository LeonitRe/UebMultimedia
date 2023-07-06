<template>
  <div class="d-flex align-items-center cont w-100">
    <div class="infographic-container w-25" ref="container"></div>
    <div class="color-container w-25">
      <div
        v-for="(category, index) in infographicData"
        :key="index"
        class="color"
        :style="{ backgroundColor: getCategoryColor(category.color) }"
        @click="selectCategory(category)"
      ></div>
    </div>
    <div class="statistics-container w-25" v-if="selectedCategory">
      <h2 class="text-dark">{{ selectedCategory.name }}</h2>
      <p>High Score: {{ selectedCategory.highScore }}</p>
      <p>Levels Completed: {{ selectedCategory.levelsCompleted }}</p>
      <p>Play Time: {{ selectedCategory.playTime }}</p>
    </div>
    <div
      class="w d-flex justify-content-center align-items-center h-100 w-25"
      v-if="selectedCategory"
    >
      <img class="h-100 w-100" :src="selectedCategory.image" :alt="selectedCategory.name" />
    </div>
  </div>
</template>

<style scoped>
.infographic-container {
  width: 400px;
  height: 300px;
  position: relative;
}

.infographic-label {
  position: absolute;
  font-size: 12px;
  font-weight: bold;
  color: #333;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
  pointer-events: none;
}

.infographic-value {
  position: absolute;
  font-size: 14px;
  font-weight: bold;
  color: #fff;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
  pointer-events: none;
}

.infographic-graph {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 0;
  background-color: #333;
  transition: height 0.3s ease-in-out;
}

.infographic-category {
  border: 2px solid transparent;
  border-radius: 50%;
  cursor: pointer;
  transition: border-color 0.3s ease-in-out;
}

.infographic-category.selected {
  border-color: #333;
}

.statistics-container {
  margin-top: 20px;
}

.statistics-container h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

.statistics-container p {
  font-size: 14px;
  margin: 5px 0;
}

.color-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.color {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin: 0 10px;
  cursor: pointer;
}
.cont {
  height: 70vh;
}
</style>

<script setup>
import * as PIXI from 'pixi.js'
import { onMounted, reactive, ref } from 'vue'

const infographicData = [
  {
    label: 'Category 1',
    value: 30,
    color: 0xff0000,
    name: 'Pacman',
    highScore: 5000,
    levelsCompleted: 5,
    playTime: '2 hours',
    image:
      'https://media3.giphy.com/media/d9QiBcfzg64Io/giphy.gif?cid=6c09b952l5mn1zw1jho4l18tfxpfnrv13bawbwzw6vwqhxbs&ep=v1_gifs_search&rid=giphy.gif&ct=g'
  },
  {
    label: 'Category 2',
    value: 50,
    color: 0x00ff00,
    name: 'Tetris',
    highScore: 10000,
    levelsCompleted: 8,
    playTime: '1.5 hours',
    image: 'https://i.gifer.com/origin/c1/c12786ec5d84e90eedebaeb4d96447f5_w200.gif'
  },
  {
    label: 'Category 3',
    value: 20,
    color: 0x0000ff,
    name: 'Mario',
    highScore: 8000,
    levelsCompleted: 6,
    playTime: '2.5 hours',

    image: 'https://www.invajy.com/wp-content/uploads/2018/05/SuperMarioBrosGIF.gif'
  }
]

const container = ref(null)
let app, graphics, labels, graph, categories

const selectedCategory = reactive({
  name: '',
  highScore: '',
  levelsCompleted: '',
  playTime: ''
})

onMounted(() => {
  app = new PIXI.Application({ width: 400, height: 300, backgroundColor: 0xffffff })
  container.value.appendChild(app.view)

  graphics = new PIXI.Graphics()
  app.stage.addChild(graphics)

  labels = []

  drawInfographic()
})

function drawInfographic() {
  const totalValue = infographicData.reduce((acc, data) => acc + data.value, 0)
  let startAngle = -Math.PI / 2

  categories = []

  infographicData.forEach((data) => {
    const angle = (data.value / totalValue) * Math.PI * 2
    const endAngle = startAngle + angle

    graphics.beginFill(data.color)
    graphics.moveTo(200, 150)
    graphics.arc(200, 150, 100, startAngle, endAngle)
    graphics.lineTo(200, 150)
    graphics.endFill()

    const labelX = 200 + Math.cos(startAngle + angle / 2) * 100
    const labelY = 150 + Math.sin(startAngle + angle / 2) * 100
    const valueX = 200 + Math.cos(startAngle + angle / 2) * 80
    const valueY = 150 + Math.sin(startAngle + angle / 2) * 80

    const label = new PIXI.Text(data.label, { fill: '#333', fontSize: '12px', fontWeight: 'bold' })
    label.position.set(labelX, labelY)
    label.anchor.set(0.5)
    label.alpha = 0
    labels.push(label)
    app.stage.addChild(label)

    const value = new PIXI.Text(data.value.toString(), {
      fill: '#fff',
      fontSize: '14px',
      fontWeight: 'bold'
    })
    value.position.set(valueX, valueY)
    value.anchor.set(0.5)
    value.alpha = 0
    labels.push(value)
    app.stage.addChild(value)

    const category = new PIXI.Graphics()
    category.beginFill(data.color, 0.8)
    category.arc(200, 150, 100, startAngle, endAngle)
    category.lineTo(200, 150)
    category.endFill()
    category.interactive = true
    category.buttonMode = true
    categories.push(category)
    app.stage.addChild(category)

    startAngle += angle
  })

  graph = new PIXI.Graphics()
  app.stage.addChild(graph)
}

function selectCategory(category) {
  categories.forEach((cat) => {
    cat.removeClass = false
    cat.lineStyle(2, cat.defaultLineColor)
  })

  const selectedCategoryIndex = infographicData.indexOf(category)
  const selectedCategoryObject = infographicData[selectedCategoryIndex]

  if (selectedCategoryObject) {
    selectedCategory.name = selectedCategoryObject.name
    selectedCategory.highScore = selectedCategoryObject.highScore
    selectedCategory.levelsCompleted = selectedCategoryObject.levelsCompleted
    selectedCategory.playTime = selectedCategoryObject.playTime
    selectedCategory.image = selectedCategoryObject.image // Set the image URL
  }

  graph.clear()
  graph.beginFill(0x333333)
  graph.drawRect(0, graphY, 400, graphHeight)
  graph.endFill()

  labels.forEach((label) => {
    label.alpha = 0
  })

  const selectedLabel = labels.find((lbl) => lbl.text === category.label)
  if (selectedLabel) {
    selectedLabel.alpha = 1
  }

  category.addClass('selected')
}

function getCategoryColor(color) {
  return PIXI.utils.hex2string(color)
}
</script>
