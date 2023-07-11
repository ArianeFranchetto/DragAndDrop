<script>
import { ref } from 'vue';

export default {
  setup () {
    const items = ref ([
    {id: 0, title: 'Item A', list: 1},
    {id: 1, title: 'Item B', list: 1},
    {id: 2, title: 'Item C', list: 1},
    {id: 3, title: 'Item D', list: 1},
    {id: 4, title: 'Item E', list: 1},
    {id: 5, title: 'Item F', list: 1},
  
    
    ])
  
const getList = (list) => {
  return items.value.filter((item) => item.list == list)
}

const startDrag = (event, item) => {
  console.log(item)
  event.dataTransfer.dropEffect = 'move'
  event.dataTransfer.effectAllowed = 'move'
  event.dataTransfer.setData('itemID', item.id)

}

const onDrop = (event, list) => {
  const itemID = event.dataTransfer.getData('itemID')
  const item = items.value.find((item) => item.id == itemID)
  item.list =  list
 
  
}

return {
  getList,
  onDrop,
  startDrag,

}

  }
}

</script>

<template>
<div class="drop-zone"
@drop="onDrop($event, 1)"
@dragenter.prevent
@dragover.prevent
>

<div><h3>Pendente</h3></div>

<div 
    v-for="item in getList(1)" 
    :key="item.id" 
    class="drag-el"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}

    </div>
</div>

<div class="drop-zone"
@drop="onDrop($event, 2)"
@dragenter.prevent
@dragover.prevent
>

<div><h3>Concluído</h3></div>
    <div 
    v-for="item in getList(2)" 
    :key="item.id" 
    class="drag-el"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}

    </div>
    </div>
</template>

<style>
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-smoothing: grayscale;
  text-align: center;
  color: beige;

}

.drop-zone {
  width: 250px;
  height: 250px;
  margin: 50px auto;
  background-color: rgb(63, 33, 60);
  padding: 10px;
  border-radius: 5px;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  flex-direction: row;


}

.drag-el {
  background-color: aquamarine;
  color: rgb(144, 92, 92);
  width: 50px;
  height: 50px;

}

.drag-el:nth-last-of-type(1) {
  margin-bottom: 0;
}

</style>
