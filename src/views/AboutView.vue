<script setup lang="ts">
import { gsap } from 'gsap'
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'
import { TextPlugin } from 'gsap/TextPlugin'
import { onMounted, ref } from 'vue'


gsap.registerPlugin(MotionPathPlugin)
gsap.registerPlugin(TextPlugin)

const title =ref<HTMLElement | null>(null)
const containerSubTitle =ref<HTMLElement[] | null>(null)
const me =ref<HTMLElement | null>(null)

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

})




//now animate each character into place from 100px above, fading in:


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
</template>

<style>
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
