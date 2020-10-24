<template>
<div class=" ">

    <Sidebar></Sidebar>
    <div class="layout container ui">

        <router-view></router-view>

    </div>
</div>
</template>

<script>
import Sidebar from '@/components/Sidebar.vue'

export default {
    name: 'app',
    components: {
        Sidebar
    }
}
</script>
