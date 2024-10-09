<script setup lang="ts">
import { gsap } from 'gsap'
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'
import { TextPlugin } from 'gsap/TextPlugin'
import { onMounted, reactive, ref } from 'vue'


gsap.registerPlugin(MotionPathPlugin)
gsap.registerPlugin(TextPlugin)

const title =ref<HTMLElement | null>(null)
const containerSubTitle =ref<HTMLElement[] | null>(null)
const me =ref<HTMLElement | null>(null)
const circleRef =ref<HTMLElement | null>(null)
  let t1 

const position = reactive({x:0,y:0})



const jump = ()=>{
  t1 = gsap.timeline({repeat: -1})
  t1.to(circleRef.value, {
            top: startJump.y, 
            duration: 0.3,
            onComplete: (target)=>{
              if( circleRef.value){
          circleRef.value.style.backgroundColor = 'red'
          }

        },  
                  }
        )
        t1.to(circleRef.value, {
            duration: 1,
            top: startJump.y - 200,       
            ease: "power1.out",            
        })
        t1.to(circleRef.value, {
            top: startJump.y,   

        onComplete: ()=>{
          if( circleRef.value){
              circleRef.value.style.backgroundColor = 'green'
          }
        
        },      
            duration: 1,
            ease: "power1.in",    
        }
        )


}



onMounted(() => {
  if (!title.value) {
    return
  }
gsap.from(title.value, {  y: -20, scaleY: 0.2, duration: 0.3 });
gsap.from(containerSubTitle.value?.children, {  
  delay: 0.5,
  x: -40,  
  stagger:0.25,
  autoAlpha: 0,
  duration: 0.4 });

gsap.from(me.value, {
  delay:2,
  duration: 2.5, 
  text: ""});

//прыжки
//   gsap.from(circleRef.value,  
//   {  y: -20, scaleY: 0.2, duration: 0.3 }
// );

jump()

})


const cssStyleForNumber = (str: string | undefined) => {
  if(str){
      return Number(str.split('px')[0])
  } else {
    return 0
  }

}


// обработка логики прыжков
interface IItem {
  x: number,
  y: number,
  width: number,
  heidth: number,
}
const arrayItems = ref<IItem[]>([{
  y: 300,
    x: 0,
    width: 100,
    heidth: 20
},
{
  y: 180,
    x: 5,
    width: 100,
    heidth: 20
}
,
{
  y: 50,
    x: -86,
    width: 100,
    heidth: 20
}
])

const stepArrayMost = ref<number>(0)

interface IStartJump {
  x: number,
y:number
}
const startJump = reactive<IStartJump>({x:10,y:400})

const nextMost = reactive<IItem>(
  {x:0,
  y:300,
  width: 100,
  heidth: 20
}
)
  let trigger = false


setInterval(()=>{
  const human = circleRef.value
  if(!human){
    return
  }

  // const positionHumanY = Number(circleRef.value?.style.top.split('px')[0])
  const positionHumanY = cssStyleForNumber(human?.style.top)
  const positionHumanX = cssStyleForNumber(human?.style.left)

if((positionHumanY + human.clientHeight) < nextMost.y){

trigger = true
}

if((positionHumanY + human.clientHeight) > nextMost.y && trigger &&  (positionHumanX + human.clientWidth) > nextMost.x &&  (positionHumanX )< nextMost.x + nextMost.width){
   console.log(arrayItems.value.length)
   stepArrayMost.value++
  trigger = false
  startJump.y = nextMost.y - human.clientHeight

  if(stepArrayMost.value < arrayItems.value.length){
      nextMost.x= arrayItems.value[stepArrayMost.value].x
  nextMost.y= arrayItems.value[stepArrayMost.value].y
  nextMost.width= arrayItems.value[stepArrayMost.value].width
  nextMost.heidth= arrayItems.value[stepArrayMost.value].heidth
  }



  // t1.pause()



  t1.kill();
  jump()
}

}, 30)







//


</script>


<template>
  <div class="about">
    <h1 ref="title" class="title">Портфолио Лебедев Аркадий</h1>
  </div>
  <div class="" ref="containerSubTitle">
    <p class="sub-title">Серия «Куриный бульон для души» славится своими историями о маленьких радостях и чудесах, на которые способны люди. В каждой книге собраны рассказы, основанные на реальных событиях. Они утешают, смешат и дарят надежду. Именно поэтому за последние четверть века «Куриный бульон» стал самой продаваемой серией в мире.</p>
    <p class="sub-title">Обзавестись бумажным антидепрессантом, исключающим любые побочные явления, можно на нашем сайте. А познакомиться с одной из новелл и того проще.</p>
    <p class="sub-title">Чтобы не быть голословной, Ольга написала книгу «Попутчица», где собрала истории, произошедшие с ней и ее близкими. Мы публикуем рассказ «Венеция», вошедший в этот сборник.</p>
  </div>
  <div class="section">
    <h1 ref="me" class="me">Немного обо мне:</h1>
  </div>

  <div class="box">
    <div class="most" v-for="item in arrayItems" :key="item.x" :style="{left: item.x + 'px', top: item.y + 'px', width: item.width + 'px', height: item.heidth + 'px'}"></div>
<div class="circle" ref="circleRef" :style="{left: startJump.x + 'px', top: startJump.y + 'px'}"></div>
  </div>
</template>

<style>

.most{
  position: absolute;   
    background: rgb(0, 7, 203);
}

.circle{
    position: absolute;
    width: 10px;
    height: 30px;
    background: red;
}

.box{
  position: relative;
  margin-top: 30px;
  width: 600px;
  height: 500px;
  border: 1px solid black;
}
.section{
  margin-top: 50px;
}

.title{
  margin-bottom: 30px;
}

.sub-title{
  margin-bottom: 15px;
}

</style>
