<script setup>
    const props = defineProps({
        ipInfo: {
            type: Object,
            required: true,
        }
    })
</script>

<template>
    <div class="absolute flex flex-col px-8 pt-8 pb-12 bg-white rounded-md -bottom-64 lg:-bottom-20 lg:flex-row gap-y-4 gap-x-12">
        <!-- flex item #1 -->
        <div class="flex flex-col">
            <h3 class="mb-2 text-xs uppercase"> IP Address</h3>
            <span class="text-2xl">{{props.ipInfo.address}}</span>
        </div>

        <!-- flex item #2 -->
        <div class="flex flex-col">
            <h3 class="mb-2 text-xs uppercase">Location</h3>
            <span class="text-2xl">{{props.ipInfo.state.region}}</span>
        </div>

        <!-- flex item #3 -->
        <div class="flex flex-col">
            <h3 class="mb-2 text-xs uppercase">Timezone</h3>
            <span class="text-2xl">{{props.ipInfo.timezone}} UTC</span>
        </div>

        <!-- flex item #1=4 -->
        <div class="flex flex-col">
            <h3 class="mb-2 text-xs uppercase">ISP</h3>
            <span class="text-2xl">{{props.ipInfo.isp}}</span>
        </div>
    </div>
</template>