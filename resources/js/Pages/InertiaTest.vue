<script setup>
import { Link } from '@inertiajs/inertia-vue3';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: String,
    phpVersion: String,
});
</script>

<template>
Inertiaテストです。<br>
<a href="/">aタグ経由です</a><br>
<Link href="/">Linkタグ経由です</Link>

</template>
