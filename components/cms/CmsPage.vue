<script setup lang="ts">
import {CmsPage, CmsSection} from "@shopware-pwa/types";
import {Splide, SplideSlide} from '@splidejs/vue-splide';
import '@splidejs/vue-splide/css';

const props = defineProps<{
    content: CmsPage;
}>();

const cmsSections = computed<CmsSection[]>(() => {
    return props.content?.sections || [];
});

const slideOptions = {
    video: {mute: true, hideControls: true, autoplay: true},
    isNavigation: false,
    pagination: false,
    arrows: false,
    rewind: true,
    autoplay: true,
    pauseOnHover: false,
    pauseOnFocus: false,
    drag: false,
    height: "100vh",
};

function addStyle(section: { backgroundMedia: { url: any; }; backgroundColor: any; }) {
    let style = "";
    if (section.backgroundMedia?.url) {
        style += `background-image: url('${section.backgroundMedia?.url}')`;
    }
    if (section.backgroundColor) {
        style += `background-color: ${section.backgroundColor}`;
    }
    return style
}
</script>

<template>
    <Splide :options="slideOptions">
        <template v-for="section in cmsSections">
            <SplideSlide
                    data-splide-interval="1500"
                    class="splide-slide-item"
                    :style="addStyle(section)"
                  >
                <div >
                    {{ section._uniqueIdentifier }}
                </div>
            </SplideSlide>
        </template>
    </Splide>
</template>

<style>
.splide-slide-item {
    display: flex;
    justify-content: center;
    align-items: center;
    background-size: cover;
}
</style>
