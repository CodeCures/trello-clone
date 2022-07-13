<script setup lang="ts">
    defineProps(['board']);
</script>

<template>
    <div class="w-[230px] h-[200px] border-[1px] border-gray-300 rounded-md overflow-hidden">
        <div class="h-[80%]">
            <img src="https://images.unsplash.com/photo-1469474968028-56623f02e42e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2948&q=80" alt="">
        </div>
        <p>{{ board.id }}</p>
        <h4 class="px-3">{{ board.title }}</h4>
    </div>
</template>