<script setup>
import { Inertia } from '@inertiajs/inertia'

defineProps({
    id :  String,
    blog : Array,
})

const deleteFunction = id => {
    Inertia.delete(`/inertia/${id}`, { 
        onBefore: () => confirm('本当に削除しますか？')
    })
}

</script>

<template>{{ id }}<br>
    {{ blog.title }}
<button @click="deleteFunction(blog.id)">削除</button>
</template>