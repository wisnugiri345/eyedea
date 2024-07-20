<script setup>
import {
  onMounted,
  ref,
  toRefs,
} from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { data } from './data';

gsap.registerPlugin(ScrollTrigger);

const samurai = ref();

const props = defineProps(['stepActive']);

const { stepActive } = toRefs(props);

const animateValueChange = (newValue, oldValue) => {
  gsap.fromTo(
    '.year',
    { opacity: 0, y: -20 },
    { opacity: 1, y: 0, duration: 0.5 },
  );
};

onMounted(() => {
  // wood 2 Right
  gsap.to(samurai.value, {
    scale: 0.8,
    translateY: -100,
    scrollTrigger: {
      trigger: samurai.value,
      start: 'bottom 120%',
      end: 'bottom 30%',
      scrub: true,
    },
  });
});
</script>

<template>
  <section>
    <div
      class="content fixed w-screen h-screen box-border border-x-[50px] border-t-[10px] border-b-[200px] border-[#e6e6e6]"
    >
      <div class="logo bg-[#e6e6e6] w-fit p-5 rounded-br-[20px]">
        <img src="../../assets/img/eyedea.png" alt="logo" />
      </div>
      <div
        class="samurai flex justify-center -bottom-[100px] left-auto right-auto relative"
        ref="samurai"
      >
        <img src="../../assets/img/Samurai-2 1.png" alt="Samurai" />
      </div>
      <div
        class="year font-['Against'] text-[#CED2D4] absolute bottom-[-180px] right-[10px] text-[120px] transition ease-in-out"
      >
        {{ data[stepActive - 1].year }}
      </div>
      <div
        class="steps absolute bottom-0 bg-[#e6e6e6] flex items-center gap-[30px] rounded-tr-[20px] py-[10px] px-[50px]"
      >
        <div
          @click="stepActive !== i && $emit('changeStep', i)"
          :class="stepActive === i ? 'dot-big' : 'dot-small cursor-pointer'"
          class="rounded-full flex items-center justify-center font-['Against'] hover:bg-[#444]"
          v-for="i in 4"
          :key="stepActive * 10 + i"
        >
          {{ stepActive === i ? stepActive : '' }}
        </div>
      </div>
      <div class="description absolute top-[100%] text-[#111]">
        <div class="head font-['Mondapick'] text-[50px]">
          {{ data[stepActive - 1].city }}
        </div>
        <div class="font-['Geomatrix'] text-[14px] w-1/3">
          {{ data[stepActive - 1].description }}
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.dot-small {
  height: 20px;
  width: 20px;
  background: #dfdfdf;
  border: 1px solid #ccc;
  color: #ccc;
}
.dot-big {
  height: 40px;
  width: 40px;
  background: #1f1f1f;
}
</style>
