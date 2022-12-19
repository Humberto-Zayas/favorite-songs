<template>
  <div class="carousel-container">
    <Carousel @slide-start="handleSlideStart" @slide-end="handleSlideEnd" @loop="handleLoop" id="gallery" :autoplay="20000" :items-to-show="1"
      :wrap-around="true" :transition="1000" v-model="currentSlide">
      <Slide
        :style="`background-image: linear-gradient(0deg, rgba(0,0,0,1) 4%, rgba(0,0,0,0.5) 80%, rgba(0,0,0,0.3) 100%), url(${song.image})`"
        class="backdrop" v-for="(song, index) in favoriteSongs" :key="song.id">
        <Transition>
          <h2 style="font-weight: bold" class="carousel__item">{{ index + 1 }}. {{ song.name }}</h2>
        </Transition>
        <div style="height: 100px; width: 80%">
          <Transition>
            <div v-if="showOne" class="carousel__item">{{ song.reasons[0] }} </div>
          </Transition>
        </div>
        <div style="height: 100px; width: 80%">
          <Transition>
            <div v-if="showTwo" class="carousel__item">{{ song.reasons[1] }} </div>
          </Transition>
        </div>
        <div style="height: 100px; width: 80%">
          <Transition>
            <div v-if="showThree" class="carousel__item">{{ song.reasons[2] }} </div>
          </Transition>
        </div>
      </Slide>
    </Carousel>

    <Carousel @slide-start="handleSlideStart" @slide-end="handleSlideEnd" id="thumbnails" :items-to-show="3.5"
      :wrap-around="true" v-model="currentSlide" ref="carousel">
      <Slide :style="`background-image: url(${slide.image});`" v-for="slide in favoriteSongs"
        :class="'galla galla' + slide.id" :itemsToShow="3.95" :key="slide.id">
        <div class="carousel__item" @click="slideTo(slide.id - 1)">{{ slide.name }}</div>

      </Slide>
    </Carousel>
  </div>
</template>
 
<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.backdrop {
  background-position: bottom left;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  height: 75vh;
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
import { Howl, Howler } from 'howler';

import { defineComponent, Transition } from 'vue'
import { Carousel, Slide } from 'vue3-carousel'

import nervosa2 from '../assets/images/nervosa2.png'
import warm from '../assets/images/warm.png'
import hypochondriac from '../assets/images/hypochondriac.png'
import brakence2 from '../assets/images/brakence2.png'
import argyle from '../assets/images/argyle.png'

import 'vue3-carousel/dist/carousel.css'
import router from '@/router';

export default defineComponent({
  name: 'Gallery',
  components: {
    Carousel,
    Slide,
  },
  data: () => ({
    show: false,
    showOne: false,
    showTwo: false,
    showThree: false,
    currentSlide: 0,
    currentSong: null,
    previousSong: '',
    favoriteSongs: [
      {
        name: 'Warm',
        id: 1,
        image: warm,
        src: ['/music/warm.mp3'],
        howl: null,
        reasons: [
          'I never heard this combo of RnB and glitch, I ruv it',
          'I love you love Brakence, you have good taste in moosic',
          'He really has somethign for everyone imo'
        ]
      },
      {
        name: 'Brakence 2.0 Freestyle',
        id: 2,
        image: brakence2,
        src: ['/music/brakence.mp3'],
        howl: null,
        reasons: [
          'Some of my favorite lines are thrown out on this track',
          '"Eat fuck and make beats then I fall backwards" - singing my life with his words',
          '"She said she wanna fuck with a synth nerd from the suburbs" - damn!'
        ]
      },
      {
        name: 'Argyle',
        id: 3,
        image: argyle,
        src: ['/music/argyle.mp3'],
        howl: null,
        reasons: [
          'Maybe not the best song to put in here to you, but it\'s real',
          'The torment of dealing with/pushing away love and finding where shit in your life sits and whatnot',
          'I guess it\'s all part of the story, idk I think too much tho'
        ]
      },
      {
        name: 'Hypochondriac',
        id: 4,
        image: hypochondriac,
        src: ['/music/hypochondriac.mp3'],
        howl: null,
        reasons: [
          'First of all the entire album is fire and I love every song',
          'This one is really sweet and if I had to pick one to you this would be it',
          '<3'
        ]
      },
      {
        name: 'Nervosa2',
        id: 5,
        image: nervosa2,
        src: ['/music/nervosa2.mp3'],
        howl: null,
        reasons: [
          'This was the first song by him you sent me to me',
          'At first I didn\'t like it at all, but now I ruv it',
          'It always reminds me of when we first started talking more'
        ]
      }
    ]
  }),
  methods: {
    handleLoop() {
      console.log('Looping');
      this.currentTrack.stop();
      this.$router.push('/about')
    },
    resetShows() {
      this.showOne = false;
      this.showTwo = false;
      this.showThree = false;
    },
    startShows() {
      setTimeout(() => {
        this.showOne = true
      }, 2000)

      setTimeout(() => {
        this.showTwo = true
      }, 6000)

      setTimeout(() => {
        this.showThree = true
      }, 11000)
    },
    slideTo(val: number) {
      this.currentTrack.stop();
      this.currentSlide = val
    },
    handleSlideStart(data: any) {
      
      this.currentTrack.stop()
      this.resetShows();
    },
    handleSlideEnd(data: any) {
      this.startShows();
      if (!this.currentTrack.playing()) {
        console.log(this.currentTrack.playing())
        
       
        this.currentTrack.play()
        
      }

      this.startShows()

      
    }
  },
  mounted: function () {
    this.currentTrack.play();
    setTimeout(() => {
      this.showOne = true
    }, 1000)

    setTimeout(() => {
      this.showTwo = true
    }, 5000)

    setTimeout(() => {
      this.showThree = true
    }, 10000)

  },
  computed: {
    currentTrack() {
      var sound = new Howl({
        src: this.favoriteSongs[this.currentSlide].src,
        html5: true,
      })
      return sound;
    }
  }
})
</script>
