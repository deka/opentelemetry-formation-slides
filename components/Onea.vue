<template>
    <div class="flex items-center cursor-pointer" @click="goto">
        <img src="/images/logo-cercle.png" class="w-6" />
        <span class="ml-2 text-[#3C9B96] font-bold text-2xl">ONEA</span>
    </div>
</template>

<script setup lang="ts">
const goto = () => {
    window.open('https://www.linkedin.com/in/dimitri-rayer/', '_blank');
}
</script>

<style scoped>

</style>