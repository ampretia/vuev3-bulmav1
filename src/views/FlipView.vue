<script setup lang="ts">
import { computed, reactive, ref } from 'vue';

type CellData = {
  title: string,
  text: string,
  flipped: boolean,
  count: 0
}

const numberCells = 15;
let cd: CellData[] = []
for (let x = 0; x < numberCells; x++) {
  const d: CellData = {
    title: `Cell ${x}`,
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ornare magna eros, eu pellentesque",
    flipped: false,
    count: 0
  }
  cd.push(d as any)
}

let cdd: any = []
for (let i = 0; i < cd.length; i += 6) {
  cdd.push(cd.slice(i, i + 6))
}


const cellData = ref(cdd)

let cellFlipped = ref(true);

const flip = computed(() => {
  return cellFlipped.value ? 'rotateY(0deg)' : 'rotateY(180deg)'
})


const visible = computed(() => {
  return cellFlipped.value ? 'visible' : 'hidden'
})

const ivisible = computed(() => {
  return !cellFlipped.value ? 'visible' : 'hidden'
})

// const flip = reactive({
//   transform: 'rotateY(0deg)'
// })

function flipCard() {
  cellFlipped.value = !cellFlipped.value
}

function count(cell: CellData) {
  cell.count++;

}

</script>


<template>

  <div class="gridflip">

    <div class="section">
      <div class="container">

        <div class="container" v-for="(row, ri) in cellData" :key="ri">

          <div class="columns">
            <div v-for="(cell, index) in row" :key="index" @click="count(cell)" class="">

              <div class="column">
                <div class="flip-card-inner">
                  <div class="flip-card-front box has-background-primary">
                    <p class="title">{{ cell.title }}</p>
                    <p> {{ cell.text }}</p>
                    <p> {{ cell.flipped }}</p>
                    <p> Clicked {{ cell.count }} times</p>
                  </div>
                  <div class="flip-card-back box">
                    <p class="title"> Back of {{ cell.title }}</p>
                    <p> {{ cell.text }}</p>
                    <p> {{ cell.flipped }}</p>
                    <p> Clicked {{ cell.count }} times</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>


      </div>
    </div>

  </div>
</template>

<style>
/* The flip card container - set the width and height to whatever you want. We have added the border property to demonstrate that the flip itself goes out of the box on hover (remove perspective if you don't want the 3D effect */
.flip-card {

  /* Remove this if you don't want the 3D effect */

}

/* This container is needed to position the front and back side */
.flip-card-inner {
  perspective: 1000px;
  position: relative;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Position the front and back side */
.flip-card-front,
.flip-card-back {
  margin: 0;
  display: block;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  -webkit-backface-visibility: hidden;
  /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  transform: rotateX(0deg) rotateY(0deg);
}

/* Style the back side */
.flip-card-back {
  transform: rotateY(180deg);
}
</style>
