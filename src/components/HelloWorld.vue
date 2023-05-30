<template>
  <h1>{{ msg }}</h1>

  <v-item-group
      v-model="model"
      class="d-flex justify-sm-space-between px-0 pt-2 pb-6"
  >
    <v-item
        v-for="(fruit, index) in fruits"
        :key="index"
    >
      <v-btn
          icon
          :active="true"
          border
          height="50"
          variant="text"
          width="50"
          style="background-color: #d2d2d2 !important"
          @click="toggleFruit(index)"
      >
        <v-img
            :src="`fruit/${fruit}${activeFruits.includes(index) ? '_color' : ''}.svg`"
            width="30"
            height="30"
        />
      </v-btn>
    </v-item>
  </v-item-group>
</template>

<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()
const model = ref(null)

const fruits = ref([
    'apple', 'avocado', 'banana', 'cherry', 'grape', 'lemon', 'pear', 'strawberry', 'watermelon'
])

const activeFruits = ref([])

function toggleFruit (index: Number) {
  if (activeFruits.value.includes(index)) {
    activeFruits.value = activeFruits.value.filter(obj => { return obj !== index })
  } else {
    activeFruits.value.push(index)
  }
}
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
