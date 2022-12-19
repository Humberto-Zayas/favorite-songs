<template>
  <div class="carousel-container">
    <Carousel id="gallery" :autoplay="10000" :items-to-show="1" :wrap-around="true" :transition="1000" v-model="currentSlide" @slide-start="handleSlideStart" @slide-end="handleSlideEnd">
      <Slide :style="`background-image: linear-gradient(0deg, rgba(0,0,0,1) 4%, rgba(0,0,0,0.5) 80%, rgba(255,255,255,0.06068364845938379) 100%), url(${song.image})`" class="backdrop" v-for="song in favoriteSongs" :key="song.id">
        <div class="carousel__item">{{ song.name }} | {{ song.id }} </div>
      </Slide>
    </Carousel>

    <Carousel id="thumbnails" :items-to-show="3.5" :wrap-around="true" v-model="currentSlide" ref="carousel">
      <Slide :style="`background-image: url(${slide.image});`" v-for="slide in favoriteSongs" :class="'galla galla' + slide.id" :itemsToShow="3.95" :key="slide.id">
        <div class="carousel__item" @click="slideTo(slide.id - 1)">{{ slide.name }}</div>

      </Slide>
    </Carousel>
  </div>
</template>

<style>
.backdrop {
  background-position: bottom left;
}
.carousel-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  padding-bottom: 3em;
}
.galla {
  background-size: cover;
}

#gallery {
  height: 75vh;
}


.galla1 {
  background-color: rgb(0, 115, 255);
  min-height: 20vh;
}

.galla2 {
  background-color: rgb(200, 41, 248);
  min-height: 20vh;
}

.galla3 {
  background-color: rgb(248, 41, 158);
  min-height: 20vh;
}

.galla4 {
  background-color: rgb(248, 75, 41);
  min-height: 20vh;
}

.galla5 {
  background-color: rgb(248, 210, 41);
  min-height: 20vh;
}

.carousel__slide {
  padding: 5px;
}

.carousel__viewport {
  perspective: 2000px;
  height: 100%;
}

.carousel__track {
  transform-style: preserve-3d;
  height: 100%;
}

.carousel__slide--sliding {
  transition: 0.5s;
}

.carousel__slide {
  opacity: 0.9;
  transform: scale(0.9);
  z-index: 0;
}

.carousel__slide--active~.carousel__slide {
  /* transform: rotateY(20deg) scale(0.9); */
  /* z-index: 10; */
}

.carousel__slide--prev {
  opacity: 1;
  transform: scale(0.95);
}

.carousel__slide--next {
  opacity: 1;
  transform: scale(0.95);
}

.carousel__slide--active {
  opacity: 1;
  transform: scale(1.14);
  z-index: 1;
  box-shadow: 0px 0px 10px 10px rgba(0, 0, 0, 0.56);
}
</style>

<script lang="ts">
import {Howl, Howler} from 'howler';

import { defineComponent } from 'vue'
import { Carousel, Slide } from 'vue3-carousel'

import nervosa2 from '../assets/images/nervosa2.png'
import warm from '../assets/images/warm.png'
import hypochondriac from '../assets/images/hypochondriac.png'
import brakence2 from '../assets/images/brakence2.png'
import argyle from '../assets/images/argyle.png'

import 'vue3-carousel/dist/carousel.css'

export default defineComponent({
  name: 'Gallery',
  components: {
    Carousel,
    Slide,
  },
  data: () => ({
    currentSlide: 0,
    nervosa2: nervosa2,
    favoriteSongs: [
      {
        name: 'Warm',
        id: 1,
        image: warm,
        src: ['/music/warm.mp3'],
        reasons: [
          'Reason one',
          'Reason two',
          'Reason three'
        ]
      },
      {
        name: 'Brakence 2.0 Freestyle',
        id: 2,
        image: brakence2,
        src: ['/music/brakence.mp3'],
        reasons: [
          'Reason one',
          'Reason two',
          'Reason three'
        ]
      },
      {
        name: 'Argyle',
        id: 3,
        image: argyle,
        src: ['/music/argyle.mp3'],
        reasons: [
          'Reason one',
          'Reason two',
          'Reason three'
        ]
      },
      {
        name: 'Hypochondriac/Introvert',
        id: 4,
        image: hypochondriac,
        src: ['/music/hypochondriac.mp3'],
        reasons: [
          'Reason one',
          'Reason two',
          'Reason three'
        ]
      },
      {
        name: 'Nervosa2',
        id: 5,
        image: nervosa2,
        src: ['/music/nervosa2.mp3'],
        reasons: [
          'Reason one',
          'Reason two',
          'Reason three'
        ]
      }
    ]
  }),
  methods: {
    slideTo(val: number) {
      this.currentSlide = val
    },
    handleSlideStart(data: any) {
      // this.$Progress.start();
      console.log('song to start: ', this.favoriteSongs[this.currentSlide].name)
      var sound = new Howl({
        src: ['/music/nervosa2.mp3'],
        html5: true
      });

      // sound.play();
      // sound.fade(0, 1, 2000);

      // setTimeout(() => {

      //   sound.fade(1, 0, 2000);
      // }, 9000)

      // setTimeout(() => {

      //   sound.stop(0);
      // }, 10000)

    },
    handleSlideEnd(data: any) {
      // console.log('song to end:', this.favoriteSongs[this.currentSlide -1].name)
    }
  },
})
</script>
