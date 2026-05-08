<template>
    <swiper :pagination="true" :modules="modules" class="slider-wrapper">
        <swiper-slide v-for="(image, index) in images" :key="index" class="slider-slide">
            <img :src="image" alt="" class="slider-image">
        </swiper-slide>
    </swiper>
</template>
<script>
import { Swiper, SwiperSlide } from 'swiper/vue';

import 'swiper/css';
import 'swiper/css/pagination';

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

<style scoped>
.slider-wrapper {
    width: 100%;
    height: 100%;
}

.slider-slide {
    width: 100%;
    display: flex;
    justify-content: center;
}

.slider-image {
    width: 100%;
    height: 16rem;
    object-fit: cover;
    border-radius: 0.75rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

@media (min-width: 768px) {
    .slider-image {
        height: 25rem;
    }
}
</style>