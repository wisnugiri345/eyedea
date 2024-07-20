<script setup>
import { computed, onMounted, provide, ref, watch } from 'vue';
import Background from './components/Background.vue';
import Content from './components/Content.vue';
import gsap from 'gsap';
import ScrollToPlugin from 'gsap/ScrollToPlugin';

gsap.registerPlugin(ScrollToPlugin);

const stepActive = ref(1);
const container = ref();
const contentHeight = ref(0);
const segmentheight = ref(330);
const scrollPosition = ref(0);
const indexActive = computed(() =>
  Math.floor(scrollPosition.value / segmentheight.value),
);

const updatescrollPosition = () => {
  scrollPosition.value = window.scrollY;
};

window.addEventListener('scroll', updatescrollPosition);
const changeStep = (e) => {
  stepActive.value = e;

  gsap.to(window, { duration: 1, scrollTo: segmentheight.value * (e - 1) });
};

watch(indexActive, (newval) => {
  stepActive.value = newval + 1 > 4 ? 4 : newval + 1;
});

onMounted(() => {
  contentHeight.value = container.value.clientHeight;
});
</script>

<template>
  <div class="content" ref="container">
    <Background :stepActive="stepActive" class="hidden lg:flex" />
    <Content
      @changeStep="changeStep"
      :stepActive="stepActive"
      class="hidden lg:flex"
    />
    <div
      class="text-[30px] flex lg:hidden font-['Against'] h-screen w-full items-center px-10 justify-center text-[#222] text-center"
    >
      Please consider using a larger screen size for an optimal viewing
      experience
    </div>
    <div class="h-[2000px]"></div>
  </div>
</template>

<style scoped>
.content {
  min-height: 100vh;
  background-image: url('../assets/img/f3aefe6c49dbf644f84f2fc5b8b45e26.png');
  background-attachment: fixed;
  background-color: #c3c1bf;
}
</style>
