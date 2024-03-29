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
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, onMounted, onUnmounted } from 'vue'
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

    const showOne = ref(false);
    const showTwo = ref(false);
    const showThree = ref(false);
    const currentSlide = ref(0);

    const currentTrack = computed(() => {
      return new Howl({
        src: favoriteSongs[currentSlide.value].src,
        html5: true,
      });
    });

    function handleLoop() {
      console.log('Looping');
      currentTrack.value.stop();
      // You may need to adjust this part according to your routing logic
      // this.$router.push('/about');
    }

    function resetShows() {
      showOne.value = false;
      showTwo.value = false;
      showThree.value = false;
    }

    function startShows() {
      setTimeout(() => {
        showOne.value = true;
      }, 2000);

      setTimeout(() => {
        showTwo.value = true;
      }, 6000);

      setTimeout(() => {
        showThree.value = true;
      }, 11000);
    }

    function slideTo(val: number) {
      currentTrack.value.stop();
      currentSlide.value = val;
    }

    function handleSlideStart() {
      currentTrack.value.stop();
      resetShows();
    }

    function handleSlideEnd() {
      startShows();
      if (!currentTrack.value.playing()) {
        currentTrack.value.play();
      }
    }

    onMounted(() => {
      currentTrack.value.play();
      setTimeout(() => {
        showOne.value = true;
      }, 1000);

      setTimeout(() => {
        showTwo.value = true;
      }, 5000);

      setTimeout(() => {
        showThree.value = true;
      }, 10000);
    });

    onUnmounted(() => {
      console.log('unmounting');
      currentTrack.value.stop();
      currentSlide.value = 0;
    });

    return {
      start: startSrc,
      finish: finishSrc,
      showOne,
      showTwo,
      showThree,
      currentSlide,
      handleLoop,
      handleSlideStart,
      handleSlideEnd,
      slideTo,
      favoriteSongs, // Expose favoriteSongs
    };
  },
});
</script>
