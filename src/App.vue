<script setup>
import NavArea from './components/NavArea.vue'
import SwiperSlide from './components/SwiperSlide.vue'
import CommonFunctionContainer from './components/CommonFunctionContainer.vue'
import SearchInputContainer from './components/SearchInputContainer.vue'
import InteractiveSituation from './components/InteractiveSituation.vue'
import ProductAreaContainer from './components/ProductAreaContainer.vue'
import PopularEvents from './components/PopularEvents.vue'
import VideoArea from './components/VideoArea.vue'
import Announcement from './components/Announcement.vue'
</script>

<template>
  <NavArea />
  <main>
    <SwiperSlide />

    <CommonFunctionContainer />
    <SearchInputContainer />

    <InteractiveSituation />
    <ProductAreaContainer />
    <PopularEvents />
    <VideoArea />
    <Announcement />
  </main>
  <footer></footer>
</template>
