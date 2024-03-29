<template>
  <div class="carousel-container">
    <div class="fakeNav">
      <div><router-link to="/"><img :src="start"></router-link></div>
      <div><router-link to="/about"><img :src="finish"></router-link></div>
    </div>
    <Carousel @slide-start="handleSlideStart" @slide-end="handleSlideEnd" @loop="handleLoop" id="gallery"
      :autoplay="22000" :items-to-show="1" :wrap-around="true" :transition="1000" v-model="currentSlide">
      <template v-for="(song, index) in favoriteSongs" :key="song.id">
        <Slide
          :style="`background-image: linear-gradient(0deg, rgba(0,0,0,1) 4%, rgba(0,0,0,0.5) 80%, rgba(0,0,0,0.3) 100%), url(${song.image})`"
          class="backdrop">
          <Transition>
            <h2 style="font-weight: bold" class="carousel__item">{{ index + 1 }}. {{ song.name }}</h2>
          </Transition>
          <div style="height: 100px; width: 80%">
            <Transition>
              <div v-if="currentSongIndex === index && showOne" class="carousel__item">{{ song.reasons[0] }} </div>
            </Transition>
          </div>
          <div style="height: 100px; width: 80%">
            <Transition>
              <div v-if="currentSongIndex === index && showTwo" class="carousel__item">{{ song.reasons[1] }} </div>
            </Transition>
          </div>
          <div style="height: 100px; width: 80%">
            <Transition>
              <div v-if="currentSongIndex === index && showThree" class="carousel__item">{{ song.reasons[2] }} </div>
            </Transition>
          </div>
        </Slide>
      </template>
    </Carousel>

    <Carousel @slide-start="handleSlideStart" @slide-end="handleSlideEnd" id="thumbnails" :items-to-show="3.5"
      :wrap-around="true" v-model="currentSlide" ref="carousel">
      <template v-for="slide in favoriteSongs" :key="slide.id">
        <Slide :style="`background-image: url(${slide.image});`"
          :class="'galla galla' + slide.id" :itemsToShow="3.95">
          <div class="carousel__item" @click="slideTo(slide.id - 1)">{{ slide.name }}</div>
        </Slide>
      </template>
    </Carousel>

    <button @click="togglePause">{{ isPaused ? 'Resume' : 'Pause' }}</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, onMounted, onUnmounted } from 'vue'
import type { Ref } from 'vue';
import { Howl } from 'howler'
import start from '../assets/images/power.svg'
import finish from '../assets/images/log-out.svg'
import { Carousel, Slide } from 'vue3-carousel'
import { favoriteSongs } from '../data/songData'
import 'vue3-carousel/dist/carousel.css'
import '@/assets/css/GalleryStyles.css';

export default defineComponent({
  name: 'Gallery',
  components: {
    Carousel,
    Slide,
  },
  setup() {
    const startSrc = start;
    const finishSrc = finish;

    const currentSlide: Ref<number> = ref(0);
    const isPaused: Ref<boolean> = ref(false);
    const currentSongIndex: Ref<number | null> = ref(null); // Track the index of the currently playing song

    let currentTrack: Howl | null = null; // Store the currently playing Howl instance

    // Play the audio for the specified song index
    function playAudio(index: number) {
      if (currentTrack) {
        currentTrack.stop(); // Stop the currently playing audio
      }
      currentSongIndex.value = index; // Update the current song index
      currentTrack = new Howl({
        src: favoriteSongs[index].src,
        html5: true,
        onend: () => {
          currentSongIndex.value = null; // Reset the current song index when audio ends
        },
      });
      currentTrack.play(); // Play the audio
    }

    function handleLoop() {
      console.log('Looping');
      if (currentTrack) {
        currentTrack.stop();
      }
      // You may need to adjust this part according to your routing logic
      // this.$router.push('/about');
    }

    function handleSlideStart() {
      if (currentTrack) {
        currentTrack.stop(); // Stop the audio when sliding to a new song
      }
    }

    function handleSlideEnd() {
      if (!isPaused.value) {
        playAudio(currentSlide.value); // Play the audio for the current slide
      }
    }

    function togglePause() {
      isPaused.value = !isPaused.value;
      if (isPaused.value && currentTrack) {
        currentTrack.pause(); // Pause the audio
      } else if (currentTrack && currentSongIndex.value !== null) {
        currentTrack.play(); // Resume playing the audio if it's paused
      }
    }

    function slideTo(val: number) {
      currentSlide.value = val;
      if (!isPaused.value) {
        playAudio(val); // Play the audio for the selected slide
      }
    }

    onMounted(() => {
      playAudio(currentSlide.value); // Play the audio for the initial slide
    });

    onUnmounted(() => {
      if (currentTrack) {
        currentTrack.stop(); // Stop the audio when the component is unmounted
      }
    });

    return {
      start: startSrc,
      finish: finishSrc,
      currentSlide,
      togglePause,
      isPaused,
      slideTo,
      favoriteSongs,
    };
  },
});
</script>
