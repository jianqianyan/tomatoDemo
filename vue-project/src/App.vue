<script setup lang="ts">
import { ref } from "vue";
import MyMenu from './components/MyMenu.vue'
const handleItemSelected = (item: any) => {
  // 在这里对返回的进行处理
  console.log(item);
}
const menuItems = ref([{ id: '1', label: '1', children: [{ id: '1.1', label: '1.1', children: [{ id: '1.1.1', label: '1.1.1', children: [] }] }] }, { id: '2', label: '2', children: [] }, {
  id: '3', label: '3'
  , children: []
}])
</script>

<template>
  <div class="menu">
    <my-menu :items="menuItems" @item-selected="handleItemSelected" />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .menu {
    width: 200px;
    /* background-color: black; */
  }
}
</style>
