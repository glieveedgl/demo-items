<script setup lang="ts">
import type { TItem } from '@/entities/Item.ts'
import { defineProps, defineEmits, computed } from 'vue'

import Selected from '@/components/items/selected.vue'
import ItemsGrid from '@/components/items/grid.vue'
import ItemsGridItem from '@/components/items/gridItem.vue'

const props = defineProps<{
  modelValue: TItem[]
  userList?: TItem[]
  selected?: TItem | null
  userSelected?: TItem[]
}>()
const emit = defineEmits([
  'update:modelValue',
  'update:userList',
  'update:selected',
  'update:userSelected',
])

const listModel = computed({
  get() {
    return props.modelValue
  },
  set(val) {
    emit('update:modelValue', val)
  },
})

const userListModel = computed({
  get() {
    return props.userList
  },
  set(val) {
    emit('update:userList', val)
  },
})

const selectedModel = computed({
  get() {
    return props.selected
  },
  set(val) {
    emit('update:selected', val)
  },
})

const userSelectedModel = computed({
  get() {
    return props.userSelected
  },
  set(val) {
    emit('update:userSelected', val)
  },
})
const maxCount = 6
const disableUserSelected = computed(() => userSelectedModel.value && userSelectedModel.value.length >= maxCount)

const onClickItem = (item: TItem, index: number) => {
  if (disableUserSelected.value || !userListModel.value) return
  const spliced = userListModel.value.splice(index, 1)
  userSelectedModel.value = (userSelectedModel.value || []).concat(spliced)
}
const onClickSelectedItem = (item: TItem, index: number) => {
  if (!userSelectedModel.value) return
  const spliced = userSelectedModel.value.splice(index, 1)
  userListModel.value = (userListModel.value || []).concat(spliced)
}
</script>
<template>
  <div class="border border-1 flex flex-col justify-stretch p-4">
    <div class="flex justify-between mb-8">
      <div class="max-w-sm w-full">
        <Selected :value="userSelectedModel">
          <template #content="slotScope">
            <ItemsGrid class="p-2 border border-1">
              <ItemsGridItem
                class="m-2"
                v-for="(selectedItem, selectedItemIndex) in slotScope.value"
                :item-data="selectedItem"
                @click="() => onClickSelectedItem(selectedItem, selectedItemIndex)"
              />
            </ItemsGrid>
            <div class="text-right font-medium">
              {{ slotScope.value.length }}/{{ maxCount }}
            </div>
          </template>
        </Selected>
      </div>
      <div>
        <Selected :value="selectedModel">
          <template #content="slotScope">
            <div
              class="min-h-[175px] min-w-[175px] font-bold border border-1 p-2 flex justify-center items-center"
            >
              {{ slotScope.value.name }}
            </div>
          </template>
        </Selected>
      </div>
    </div>
    <div class="flex flex-1">
      <div class="p-2 border border-1 border-r-0 flex-1">
        <ItemsGrid>
          <ItemsGridItem
            :disabled="disableUserSelected"
            @click="() => onClickItem(gridItem, gridItemIndex)"
            class="m-2"
            v-for="(gridItem, gridItemIndex) in userListModel"
            :item-data="gridItem"
          />
        </ItemsGrid>
      </div>
      <div class="p-2 border border-1 flex-1">
        <ItemsGrid>
          <ItemsGridItem
            @click="selectedModel = gridItem"
            class="m-2"
            v-for="gridItem in listModel"
            :item-data="gridItem"
            :class="[
              (gridItem && gridItem.id) === (selectedModel && selectedModel.id) &&
                '!bg-red-400 text-white',
            ]"
          />
        </ItemsGrid>
      </div>
    </div>
  </div>
</template>
