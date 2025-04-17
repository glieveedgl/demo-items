<script setup lang="ts">
import { defineProps } from 'vue'
import type { TItem } from '@/entities/Item.ts'

const props = defineProps<{
  itemData: TItem
  disabled?: boolean
}>()
</script>
<template>
  <div
    class="p-2 border border-2 bg-white hover:bg-gray-100 cursor-pointer"
    :class="[disabled && '!bg-gray-100 border-gray-300 text-gray-500 !cursor-not-allowed']"
  >
    <span class="font-medium">{{ itemData.name }}</span>
  </div>
</template>
