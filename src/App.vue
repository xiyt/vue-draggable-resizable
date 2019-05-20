<template>
  <div id="app">
    <input v-model="scale" />
    <div style="transform: scale(0.5);height: 500px; width: 500px; border: 1px solid red; position: relative;">
      <vue-draggable-resizable :w="400"
        :h="400"
        :parent="true"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :scale="scale">
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
  }
}
</script>

<style>
.vdr {
  border: 1px dashed black;
}
</style>
