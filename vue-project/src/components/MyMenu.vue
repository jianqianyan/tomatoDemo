<template>
    <ul>
        <menu-item v-for="item in items" :key="item.id" :label="item.label" :children="item.children" :activeId="activeId" :id="item.id"
            @item-selected="handleItemSelected" />
    </ul>
</template>
  
<script setup lang="ts">
import MenuItem from './MenuItem.vue'
import { ref, defineProps, toRef, defineEmits } from "vue";
const props = defineProps(["items"]);
const emits = defineEmits(['item-selected']);
let items = toRef(props, "items");
const activeId = ref(null);
const handleItemSelected = (item: any) => {
    activeId.value = item;
    emits('item-selected', item);
}

</script>
  