<script setup>
import { onMounted, ref, onUnmounted, inject, toRefs } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { data } from './data';

gsap.registerPlugin(ScrollTrigger);

const wood2r = ref();
const wood2l = ref();
const wood1r = ref();
const wood1l = ref();
const gate = ref();
const mount1 = ref();
const mount2 = ref();
const sun = ref();
const cities = ref();

const props = defineProps(['stepActive']);

const { stepActive } = toRefs(props);

onMounted(() => {
  // wood 2 Right
  gsap.to(wood2r.value, {
    translateX: 500,
    scrollTrigger: {
      trigger: wood2r.value,
      start: 'bottom 70%',
      end: 'bottom 30%',
      scrub: true,
    },
  });

  // wood 2 Left
  gsap.to(wood2l.value, {
    translateX: -500,
    scrollTrigger: {
      trigger: wood2l.value,
      start: 'bottom 70%',
      end: 'bottom 30%',
      scrub: true,
    },
  });

  // wood 1 Right
  gsap.to(wood1r.value, {
    translateX: 450,
    scrollTrigger: {
      trigger: wood1r.value,
      start: 'bottom 50%',
      end: 'bottom 0',
      scrub: true,
    },
  });

  // wood 1 Left
  gsap.to(wood1l.value, {
    translateX: -450,
    scrollTrigger: {
      trigger: wood1l.value,
      start: 'bottom 50%',
      end: 'bottom 0%',
      scrub: true,
    },
  });

  // Gate
  gsap
    .timeline({
      scrollTrigger: {
        trigger: gate.value,
        start: 'bottom 50%',
        end: 1200,
        scrub: true,
      },
    })
    .to(gate.value, {
      scale: 1.5,
    })
    .to(gate.value, {
      scale: 5,
      translateY: -100,
    });

  // mount 1
  gsap
    .timeline({
      scrollTrigger: {
        trigger: mount1.value,
        start: 'bottom 50%',
        end: 1200,
        scrub: true,
      },
    })
    .to(mount1.value, {
      scale: 1.3,
    });

  // mount 1
  gsap
    .timeline({
      scrollTrigger: {
        trigger: mount2.value,
        start: 'bottom 50%',
        end: 1200,
        scrub: true,
      },
    })
    .to(mount2.value, {
      scale: 1.3,
    })
    .to(mount2.value, {
      translateY: -100,
    });

  // SUN
  gsap
    .timeline({
      scrollTrigger: {
        trigger: sun.value,
        start: 'bottom 50%',
        end: 1200,
        scrub: true,
      },
    })
    .to(sun.value, {
      translateY: -100,
    })
    .to(sun.value, {
      translateY: 0,
    });
});
</script>

<template>
  <section ref="main" class="flex flex-col items-center relative">
    <div class="sun w-2/3 fixed bottom-[0px]" ref="sun">
      <img src="../../assets/img/SUN.png" class="w-full" alt="sun" />
    </div>
    <div class="mount fixed bottom-[0]" ref="mount1">
      <img src="../../assets/img/Mount-1.png" alt="mount-1" />
    </div>
    <div class="mount-2 fixed bottom-[0]" ref="mount2">
      <img src="../../assets/img/Mount-2.png" alt="mount-2" />
    </div>
    <div class="gate fixed bottom-[100px]" ref="gate">
      <img src="../../assets/img/Gate.png" alt="gate" />
    </div>
    <div class="woods-1-l flex fixed bottom-[100px] left-[0px]" ref="wood1l">
      <img src="../../assets/img/Woods 2L.png" alt="woods-1-l" />
    </div>
    <div class="woods-1-r flex fixed bottom-[100px] right-[0px]" ref="wood1r">
      <img src="../../assets/img/Woods 2R.png" alt="woods-1-r" />
    </div>
    <div
      class="city w-full h-full flex justify-center items-center fixed -mt-[100px]"
      ref="cities"
    >
      <span class="year font-['Agraham'] text-white text-[200px]">
        {{ data[stepActive - 1].city }}
      </span>
    </div>
    <div class="woods-2-l flex bottom-[150px] left-[30px] fixed" ref="wood2l">
      <img src="../../assets/img/Woods 1L.png" alt="woods-2-l" />
    </div>
    <div class="woods-2-r flex bottom-[150px] right-[30px] fixed" ref="wood2r">
      <img src="../../assets/img/Woods 1R.png" alt="woods-2-r" />
    </div>
  </section>
</template>
