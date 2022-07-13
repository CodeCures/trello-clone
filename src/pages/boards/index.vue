<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { Board } from '@/types';
import { v4 as uuidv4 } from 'uuid';
import BoardCard from '../../components/BoardCard.vue';
import { Drawer, DrawerContent } from "@progress/kendo-vue-layout";
import { Button as kbutton } from '@progress/kendo-vue-buttons';

    const boards = ref<Board[]>([]);
    let expanded = ref(true)
    let selectedId = ref();

    function handleClick() {
      expanded.value = !expanded.value;
    }

    function handleSelect(ev: any) {
      selectedId = ev.itemIndex;
      expanded.value = false;
    }
    
    const items =  [
        {
          text: "Inbox",
          icon: "k-i-inbox",
          selected: true,
        },
        {
          separator: true,
        },
        {
          text: "Notifications",
          icon: "k-i-bell",
        },
        {
          text: "Calendar",
          icon: "k-i-calendar",
        },
        {
          separator: true,
        },
        {
          text: "Attachments",
          icon: "k-i-hyperlink-email",
        },
        {
          text: "Favourites",
          icon: "k-i-star-outline",
        },
      ];
    
    const boardSchema = <Board>{
        id: uuidv4(),
        title: "My First Card",
        order: "",
        createdAt: new Date(),
        updatedAt: new Date(),
        deletedAt: new Date()
    }

    function addBoard() {
        boards.value.push(boardSchema);
    }

    onMounted(() => {
        selectedId.value = items.findIndex((x) => x.selected === true);
    })
</script>

<template>
  <div>
    <Drawer
      :expanded="expanded"
      :position="'start'"
      :mode="'push'"
      :mini="true"
      :items="
        items.map((item, index) => ({
          ...item,
          selected: index === selectedId,
        }))
      "
      @select="handleSelect"
    >
      <DrawerContent>
        <kbutton @click="handleClick">
          Toggle the drawer state
        </kbutton>
        <div class="flex space-x-5">
            <template v-if="boards.length > 0">
                <BoardCard 
                v-for="board in boards" :key="board.id"
                :board="board"
                />
            </template>
            <button @click="addBoard">New Board + </button>
        </div>
      </DrawerContent>
    </Drawer>
  </div>
</template>

<style scoped>
my-app {
  padding: 0 !important;
}
.k-drawer-content {
  padding: 20px;
}
.k-drawer-container {
  position: fixed;
  width: 100%;
  height: 100%;
}
.k-drawer-item {
  user-select: none;
}
</style>