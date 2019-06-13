<template>
  <div id="app">
    <input v-model="scale" />
    <div style="transform: scale(1);height: 500px; width: 500px; border: 1px solid red; position: relative;">
      <vue-draggable-resizable :w="100"
        :h="100"
        :parent="true"
        :debug="false"
        :min-width="100"
        :min-height="100"
        :scale="scale"
        @dragging="handleDragging">
        <p>vue-draggable-resizable</p>
      </vue-draggable-resizable>
    </div>
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'
import './components/vue-draggable-resizable.css'

export default {
  name: 'app',
  components: {
    VueDraggableResizable
  },
  data () {
    return {
      scale: 1
    }
  },
  methods: {
    handleDragging (left, top, diffX, diffY) {
      // console.log(diffX + ':' + diffY)
    }
  }
}
</script>

<style>
.vdr {
  border: 1px dashed black;
}
</style>
