<template>
    <swiper :pagination="true" :modules="modules" class="mySwiper w-full h-full">
        <swiper-slide v-for="(image, index) in images" :key="index" class="w-full flex justify-center">
            <img :src="image" alt="" class="w-full h-64 md:h-100 object-cover rounded-xl shadow-lg">
        </swiper-slide>
    </swiper>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';

// Import Swiper styles
import 'swiper/css';

import 'swiper/css/pagination';

// import './style.css';

// import required modules
import { Pagination } from 'swiper/modules';

export default {
    components: {
        Swiper,
        SwiperSlide,
    },
    props: {
        images: {
            type: Array,
            required: true,
        }
    },
    setup() {
        return {
            modules: [Pagination],
        };
    },
};
</script>