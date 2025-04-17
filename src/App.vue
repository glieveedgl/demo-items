<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'
import type { TItem } from '@/entities/Item.ts'
import Items from '@/components/items/index.vue'

const userList: Ref<TItem[]> = ref([
  {
    id: 1,
    name: 'Shoes 1',
  },
  {
    id: 2,
    name: 'Shoes 2',
  },
  {
    id: 3,
    name: 'Shoes 3',
  },
  {
    id: 4,
    name: 'Shoes 4',
  },
  {
    id: 5,
    name: 'T-shirt 1',
  },
  {
    id: 6,
    name: 'T-shirt 2',
  },
  {
    id: 7,
    name: 'T-shirt 3',
  },
  {
    id: 8,
    name: 'T-shirt 4',
  },
])
const list: Ref<TItem[]> = ref([
  {
    id: 11,
    name: 'Jacket 1',
  },
  {
    id: 12,
    name: 'Jacket 2',
  },
  {
    id: 13,
    name: 'Jacket 3',
  },
  {
    id: 14,
    name: 'Jacket 4',
  },
  {
    id: 15,
    name: 'Hoodie 1',
  },
  {
    id: 16,
    name: 'Hoodie 2',
  },
  {
    id: 17,
    name: 'Hoodie 3',
  },
  {
    id: 18,
    name: 'Hoodie 4',
  },
])

const selectedModel = ref(null)
const userSelectedModel = ref([])
</script>

<template>
  <main class="min-h-[100vh] flex align-stretch">
    <Items
      v-model:userList="userList"
      v-model="list"
      v-model:selected="selectedModel"
      v-model:userSelected="userSelectedModel"
      class="flex-1 m-2"
    />
  </main>
</template>

<style scoped></style>
