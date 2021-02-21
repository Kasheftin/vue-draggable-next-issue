<template>
  <div>
    <p>Try to move the 0-th item to the 1-th position. It fails.</p>
    <draggable
      :list="ids"
      @change="updateOrder"
    >
      <div 
        v-for="id in ids"
        :key="id"
        class="item"
      >
        {{ id }}
      </div>
    </draggable>
  </div>
  <div>
    <p>Try to move 0-th item to the 1-th position. It works. The only change is we provide [{ id: 1 }, { id: 2}, ...] to the :list prop instead of just [1, 2, ...]. </p>
    <draggable
      :list="objectIds"
      @change="updateOrder"
    >
      <div 
        v-for="id in ids"
        :key="id"
        class="item"
      >
        {{ id }}
      </div>
    </draggable>
  </div>
</template>

<script>
import { VueDraggableNext as draggable } from 'vue-draggable-next'

export default {
  components: {
    draggable
  },
  data () {
    return {
      ids: [1, 2, 3, 4, 5]
    }
  },
  computed: {
    objectIds () {
      return this.ids.map(id => ({ id }))
    }
  },
  methods: {
    updateOrder (event) {
      console.log('updateOrder', event)
      if (event.moved) {
        this.ids.splice(event.moved.newIndex, 0, this.ids.splice(event.moved.oldIndex, 1)[0])
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 500px;
}

.item {
  border: 1px solid #2c3e50;
  padding: 10px;
  margin: 10px;
}
</style>
