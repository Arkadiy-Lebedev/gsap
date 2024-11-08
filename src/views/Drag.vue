<script setup lang="ts">
  import { computed, reactive, ref } from 'vue'
import { VueDraggableNext } from 'vue-draggable-next'

const items = [{
  title: "Item 1",
  id: 1
},
{
title: "Item 2",
  id: 2
},
]

const items2 = [
{
  title: "Item 3",
  id: 3
},
{
title: "Item4",
  id: 4}
]

const    arr1 = ref([
          { name: "A442", id: 1 },
          { name: "C#", id: 2 },
          { name: "Java", id: 3 },
          { name: "PHP", id: 4 }
        ])

        const    arr2= ref([
        { name: "3454333", id: 5 },
          { name: "345", id: 6 },
          { name: "123", id: 7 },
          { name: "4234", id: 8 }
        ])

        const    arr3 = [
      
        ]



// const modules = reactive({
//         arr1: [
//           { name: "A442", id: 1 },
//           { name: "C#", id: 2 },
//           { name: "Java", id: 3 },
//           { name: "PHP", id: 4 }
//         ],
//         arr2: [
//           { name: "3454333", id: 5 },
//           { name: "345", id: 6 },
//           { name: "123", id: 7 },
//           { name: "4234", id: 8 }
//         ]
//       })

const   log = (event) =>{
        console.log(event)
      }





const list1 = ref([
        { name: 'John', id: 1 },
        { name: 'Joao', id: 2 },
        { name: 'Jean', id: 3 },
        { name: 'Gerard', id: 4 },
      ])
const list2 = ref([
        { name: 'Juan', id: 5 },
        { name: 'Edgard', id: 6 },
        { name: 'Johnson', id: 7 },
      ])

      const list3 = ref([

      ])


      const ifFull = computed(() => {
        if(list2.value.length>5){
          return false        
        } else {
          return true
        }


})


      const    checkMove =(event)=> {
      console.log('checkMove', event.draggedContext)
      console.log('Future index: ' + event.draggedContext.futureIndex)
    }

</script>


<template>
  <div class="drag">
    <!-- <VueDraggableNext class="dragArea list-group w-full" :list="arr1" @change="log" :move="checkMove">
      <div
        class="list-group-item bg-gray-300 m-1 p-3 rounded-md text-center"
        v-for="element in arr1"
        :key="element.id"
      >
        {{ element.name }}
      </div>
    </VueDraggableNext>
    <br/>

    <VueDraggableNext class="dragArea list-group w-full" :list="arr2" @change="log" :move="checkMove">
      <div
        class="list-group-item bg-gray-300 m-1 p-3 rounded-md text-center"
        v-for="element in arr2"
        :key="element.id"
      >
        {{ element.name }}
      </div>
    </VueDraggableNext> -->



    <div class="">
        <VueDraggableNext
          class=""
          :list="list1"
          :group="{ name: 'people', pull: 'clone', put: true }"
          :sort="true"
          @change="log"
          :move="checkMove"
        >
          <div
            class=""
            v-for="element in list1"
            :key="element.name"
          >
            {{ element.name }}
          </div>
        </VueDraggableNext>
      </div>


      <br/>


      <div class="">
        <VueDraggableNext
          class=""
          :list="list2"
          :group="{ name: 'people', put: ifFull }"
          @change="log"
          :move="checkMove"
        >
          <div
            class=""
            v-for="element in list2"
            :key="element.name"
          >
            {{ element.name }}
          </div>
        </VueDraggableNext>
      </div>

      <div class="">
        <VueDraggableNext
          class="dd"
          :list="list3"
          :group="{ name: 'people' }"
          @change="log"
          :move="checkMove"
        >
          <div
            class=""
            v-for="element in list3"
            :key="element.id"
          >
          <div>
               <h1> {{ element.name }}</h1>
          <p class="">{{ element.id }}</p>  
          </div>
       
          </div>
        </VueDraggableNext>
      </div>
{{ list3 }}


  </div>
</template>

<style>

.dd{
  width: 300px;
  height: 300px;
  background-color: bisque;
}
</style>
