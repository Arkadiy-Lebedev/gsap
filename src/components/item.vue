<script setup lang="ts">
import { onMounted, ref  } from 'vue'
import { gsap } from 'gsap'
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'

import IconEcosystem from '@/components/icons/IconEcosystem.vue'

const emit = defineEmits(['remove'])


gsap.registerPlugin(MotionPathPlugin)

const props = defineProps<{id: string, x: number, y: number, xTo: number, yTo: number }>()

const myElement4 = ref<HTMLElement | null>(null)

onMounted(() => { 

  if (myElement4.value) {
    const t1 = gsap.timeline()
    t1.to(myElement4.value, {
      duration: 1,
      motionPath: {
        path: [
          { left: props.x, top: props.y }, // Начальная точка
          { left: props.xTo - 100, top: props.yTo - 100 }, // Конечная точка
          { left: props.xTo, top: props.yTo }  // Конечная точка
        ],
        curviness: 1.5 // Степень кривизны пути
      },
    });
    t1.to(myElement4.value, {
      y: -20,
      scale: 1.2,
      opacity: 0.1,
      duration:0.5
    }
    )
    
    // gsap.to(myElement4.value, {
    //   duration: 1,
    //   motionPath: {
    //     path: [
    //       { left: props.x, top: props.y }, // Начальная точка
    //       { left: props.xTo - 100, top: props.yTo - 100 }, // Конечная точка
    //       { left: props.xTo, top: props.yTo }  // Конечная точка
    //     ],
    //     curviness: 1.5 // Степень кривизны пути
    //   },
    // })
  }

  setTimeout(() => {
    emit('remove', { id: props.id })
  }, 1500)

})



</script>


<template>
  <div ref="myElement4" class="myElement4" :style="{ left: x + 'px', top: y + 'px' }">
    <IconEcosystem/>
  </div>
</template>

<style scoped>
.myElement4 {
  position: absolute;

  /* background: rgb(93, 0, 255); */
  /* width: 25px;
  height: 25px; */
  border-radius: 50%;
}
</style>
