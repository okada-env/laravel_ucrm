<script setup>
import GuestLayout from '@/Layouts/Guest.vue';
import Label from '@/Components/Label.vue';
import Label from '@/Components/Input.vue';

const emitTest = e => console.log(e)

</script>

<template>
    <GuestLayout>
        <Lavel value="件名">
            タイトル
        </Lavel>
        <Input>
            
        </Input>

    </GuestLayout>
</template>
