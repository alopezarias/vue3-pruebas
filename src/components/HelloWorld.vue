<template>
  <!--h1>{{ msg }}</h1-->

  <v-card
      :loading="loading"
      class="mx-auto my-12 elevation-12 rounded-xl"
      max-width="374"
  >
    <template v-slot:loader="{ isActive }">
      <v-progress-linear
          :active="isActive"
          color="deep-purple"
          height="4"
          indeterminate
      ></v-progress-linear>
    </template>

    <!--v-img
        cover
        height="100"
        src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
    ></v-img-->

    <v-card-item>
      <v-card-title>Martes 30</v-card-title>

      <v-card-subtitle class="align-center">
        Mayo 2023
      </v-card-subtitle>
    </v-card-item>

    <!--v-card-text>

      <div class="my-2 text-subtitle-1">
        $ • Italian, Cafe
      </div>

      <div>Small plates, salads & sandwiches - an intimate setting with 12 indoor seats plus patio seating.</div>
    </v-card-text>

    <v-divider class="mx-4 mb-1"></v-divider>

    <v-card-title>Tonight's availability</v-card-title-->

    <div class="px-4">
      <v-chip-group v-model="selection">
        <v-item-group
            v-model="model"
            class="d-flex justify-sm-space-between flex-wrap align-center mx-5"
            style="width: 100%; overflow: hidden"
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
                class="icon-button"
                @click="toggleFruit(index)"
            >
              <v-img
                  :src="`fruit/${fruit}${activeFruits.includes(index) ? '_color' : ''}.svg`"
                  :class="activeFruits.includes(index) ? 'icon_button_paint' : 'icon_button_clear'"
                  width="35"
                  height="35"
              />
            </v-btn>
          </v-item>
        </v-item-group>
      </v-chip-group>
    </div>

    <v-divider :thickness="4" class="border-opacity-100 my-5 mx-15"></v-divider>

    <!--v-card-actions>
      <v-btn
          color="deep-purple-lighten-2"
          variant="text"
          @click="reserve"
      >
        GUARDAR
      </v-btn>
    </v-card-actions-->
  </v-card>
</template>

<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()
const model = ref(null)

const loading = ref(false)
const selection = ref(1)

function reserve () {
  loading.value = true

  setTimeout(() => {
    loading.value = false
  }, 2000)
}

const fruits = ref([
  'apple', 'banana',
  'cherry', 'pear',
  'strawberry',
  /*'avocado',  'grape', 'lemon',  'watermelon'*/
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

.v-card {
  background-color: #ababab !important;
  color: white;
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  font-weight: 400;
  color-scheme: light dark;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
}

.v-card-title {
  font-size: 1.5rem;
  font-weight: 600;
  line-height: 2rem;
  letter-spacing: 0.009375em;
  margin: 0;
}

.v-card-subtitle {
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5rem;
  letter-spacing: 0.009375em;
  margin: 0;
}

.icon-button {
  background-color: transparent !important;
  border: transparent !important;
  color: transparent;
  margin-left: 10px;
  margin-right: 10px;
}
.icon-button:hover {
  transform: perspective(1px) scale(1.2);
}
.icon_button_paint {
  /* animate with rotation */
  animation: paint 0.25s linear 0s;
}
.icon_button_clear {
  animation: erase 0.25s linear 0s;
}

@keyframes paint {
/* bright and make party, scaling to simulate painting */
  0% {
    transform: scale(1);
    filter: brightness(1);
  }
  25% {
    transform: scale(1.1);
    filter: brightness(1.1);
  }
  50% {
    transform: scale(1.2);
    filter: brightness(1.2);
  }
  75% {
    transform: scale(1.1);
    filter: brightness(1.1);
  }
  100% {
    transform: scale(1);
    filter: brightness(1);
  }
}

@keyframes erase {
/* move horizontally some times to simulate erasing */
  0% {
    transform: translateX(0px);
  }
  25% {
    transform: translateX(5px);
  }
  50% {
    transform: translateX(-5px);
  }
  75% {
    transform: translateX(5px);
  }
  100% {
    transform: translateX(0px);
  }
}
</style>
