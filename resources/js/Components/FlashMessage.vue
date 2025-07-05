<script setup>
import { usePage } from '@inertiajs/vue3';

const page = usePage();
</script>

<template>
    <div v-if="page.props.flash.status === 'success'" class="bg-blue-300 text-white p-4 rounded">
        {{ page.props.flash.message }}
    </div>
</template>
