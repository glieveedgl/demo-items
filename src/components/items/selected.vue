<script setup lang="ts">
import { defineProps, useSlots } from 'vue'
import type { TItem } from '@/entities/Item.ts'
const slots = useSlots()
const props = defineProps<{
  value: TItem[] | TItem | any
}>()
</script>
<template>
  <div v-if="slots.content">
    <slot name="content" v-if="Array.isArray(value) ? value.length : value" v-bind="{ value }" />
  </div>
  <div v-else>{{ value }}</div>
</template>
