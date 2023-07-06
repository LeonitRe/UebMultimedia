<template>
  <div class="flip-card w-75 h-25">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <slot name="image" />
        <!-- <img src="../assets/cloud.png" alt="Avatar" style="width: 300px; height: 300px" /> -->
      </div>
      <div class="flip-card-back d-flex flex-column justify-content-center">
        <h2><slot name="title" /></h2>
        <p><slot name="description" /></p>
      </div>
    </div>
  </div>
</template>
<style scoped>
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 200px;
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  background-color: transparent;
  color: black;
}

/* Style the back side */
.flip-card-back {
  background-color: transparent;
  color: white;
  transform: rotateY(180deg);
}
.transparent {
  background-color: transparent;
}
</style>
