<script setup lang="ts">
import { gsap } from 'gsap'
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'
import { v4 as uuidv4 } from 'uuid'
import { onMounted, ref } from 'vue'
import item from'../components/item.vue'

gsap.registerPlugin(MotionPathPlugin)

interface IInput {
  id: string,
  x: number,
  y: number
}

const array = ref<IInput[]>([])

const main = ref<HTMLElement | null>(null)
const myElement = ref(null)
const myElement2 = ref(null)
const myElement3 = ref<HTMLElement | null>(null)

const pxToPercent = (pxEl: number, percent: number) => {
  console.log(percent)
  console.log(pxEl)
  console.log((pxEl * percent) / 100)
  return (pxEl * percent ) / 100

}
  


onMounted(() => {
  if (!main.value) {
    return
  }


  if (myElement.value) {
      gsap.from(myElement.value, { duration: 1, x: 100 })
  }



   if (myElement3.value) {
     gsap.to(myElement3.value,     
       {
         motionPath: {
           path: [
             { left: 100, top: 200 }, // Начальная точка
             { left: 200, top: 100 }, 
             { left: pxToPercent(main.value.clientWidth, 70), top: pxToPercent(main.value.clientHeight, 60)}  // Конечная точка
           ],
           curviness: 1.5 // Степень кривизны пути
         },
       }
     )
  }
 
})

const start = () => {
  gsap.from(myElement2.value, { duration: 1, x: 100 })
  
}

const handleClick = (event: MouseEvent) => {


  const rect = main.value.getBoundingClientRect() // Получаем размеры и положение блока <main>

  // Вычисляем координаты клика относительно блока <main>
  const x = event.clientX - rect.left // Отнимаем координату левого края
  const y = event.clientY - rect.top  // Отнимаем координату верхнего края

  console.log(`Координаты клика: X = ${x}, Y = ${y}`);
  
  // const x = event.offsetX // Координата X клика
  // const y = event.offsetY // Координата Y клика
  console.log(`Координаты клика: X = ${x}, Y = ${y}`)
  array.value.push({ id: uuidv4(), x, y })
}


const remove = (obj: { id: string }) => {
  console.log(444)
  const index = array.value.findIndex(item => item.id === obj.id);
  if (index !== -1) {
    array.value.splice(index, 1); // Удаляем элемент по индексу
  }
}


</script>

<template>
  <main ref="main" class="main" @click.stop="handleClick">
    <!-- {{ array }} -->
    <button @click="start">start</button>
    <div ref="myElement">Hello, I'm animated!</div>
    <div ref="myElement2">2121 321 321 32 13 21</div>
    <div ref="myElement3" class="myElement3" @click="console.log(456454)"></div>
 

      <item @remove="remove" v-for="item in array" :key="item.id" :id="item.id" :x="item.x" :y="item.y"
        :xTo="main ? pxToPercent(main.clientWidth, 70) : 0" :yTo="main ? pxToPercent(main.clientHeight, 80) : 0">
      </item>

  </main>
</template>


<style >



.main{
  border: 1px solid black;
  position: relative;
  height: 80vh;
  width: 50vw;
}

.myElement3{
  position: absolute;
  top: 200px;
  left: 100px;
  background: red;
  width: 50px;
  height: 50px;
}



</style>