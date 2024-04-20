<script setup lang="ts">
import { computed, reactive, ref } from 'vue';

type CellData = {
  title: string,
  text: string,
  flipped: boolean,
  class: string,
  count: 0
}

const numberCells = 7;
let cd: CellData[] = []
for (let x = 0; x < numberCells; x++) {
  const d: CellData = {
    title: `Cell ${x}`,
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ornare magna eros, eu pellentesque",
    flipped: false,
    class: '',
    count: 0
  }
  cd.push(d as any)
}

const cellData = ref(cd)


function flipCard(cell: CellData) {
  if (cell.class === '') {
    cell.class = "flipped"
  } else {
    cell.class = ""
  }
}

</script>


<template>

  <div class="section">
    <div class="container">
      <p>0 1 2 3</p>

      <div class="fixed-grid has-6-cols ">
        <div class="grid">
          <template v-for="(celld, index) in cellData" :key="index">
            <div class="">
              <div class="flip-card">
                <div class="flip-card-inner" :class="celld.class" @click="flipCard(celld)">
                  <div class="cell box flip-card-front has-background-primary ">
                    <p class="title">{{ celld.title }}</p>
                    <p> {{ celld.text }}</p>
                    <p> {{ celld.flipped }}</p>
                    <p> Clicked {{ celld.count }} times</p>
                  </div>
                  <div class="cell box flip-card-back">
                    <p class="title"> Back of {{ celld.title }}</p>
                    <p> {{ celld.text }}</p>
                    <p> {{ celld.flipped }}</p>
                    <p> Clicked {{ celld.count }} times</p>
                  </div>
                </div>
              </div>
            </div>
          </template>
        </div>
      </div>



    </div>
  </div>

</template>

<style>
/* The flip card container - set the width and height to whatever you want. We have added the border property to demonstrate that the flip itself goes out of the box on hover (remove perspective if you don't want the 3D effect */
.flip-card {
  /* width: 300px; */

  height: 10rem;

  position: relative;
  perspective: 600px;
  border: 1px solid #f1f1f1;
  /* perspective: 1000px; */
  /* Remove this if you don't want the 3D effect */
}

/* This container is needed to position the front and back side */
.flip-card-inner {

  top: 0;
  width: 100%;
  height: 100%;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Position the front and back side */
.flip-card-front,
.flip-card-back {
  position: absolute;
  overflow: hidden;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  transform: rotateX(0deg) rotateY(0deg);
}

.flipped {
  transform: rotateY(180deg);
}

/* Style the back side */
.flip-card-back {
  transform: rotateY(180deg);
}
</style>
