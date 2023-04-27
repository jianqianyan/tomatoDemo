<template>
    <li :class="{ 'active': active && activeId == id, 'expanded': expanded }">
        <span @click="handleClick">{{ label }}</span>
        <ul v-if="hasChildren && expanded">
            <menu-item v-for="child in children" :key="child.id" :label="child.label" :children="child.children"
                :id="child.id" :active-id="activeId" @item-selected="handleItemSelected" />
        </ul>
    </li>
</template>
  
<script setup lang="ts">
import { ref, defineProps, toRef, computed, defineEmits } from "vue";
const props = defineProps(["label", "children", "activeId", 'id']);
const emits = defineEmits(['item-selected']);
let label = toRef(props, 'label'), children = toRef(props, 'children'), activeId = toRef(props, 'activeId'), id = toRef(props, 'id');
let active = ref(false), expanded = ref(false);

const hasChildren = computed(() => {
    return Array.isArray(children.value) && children.value.length > 0
})

const handleClick = () => {
    if (hasChildren.value) {
        expanded.value = !expanded.value
    } else {
        active.value = true;
        emits('item-selected', id.value);
    }
}

const handleItemSelected = (item: any) => {
    emits('item-selected', item)
}

</script>
  
<style scoped>
li {
    list-style: none;
}
li span{
    cursor: pointer;
}
.active {
    background-color: hsla(160, 100%, 37%, 1);
    color: white;
    transition: color 0.5s, background-color 0.5s;
}

.expanded {
    font-weight: bold;
}
</style>
  