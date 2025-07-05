<script setup>
import { Link, useForm } from '@inertiajs/vue3';

defineProps({
    errors: Object,
});

const form = useForm({
    title: '',
    content: '',
});

const submit = () => {
    form.post(route('inertia.store'));
};
</script>

<template>
    <div>
        <div class="mb-4">
            <Link :href="route('inertia.index')" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
                一覧に戻る
            </Link>
        </div>
        
        <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <h1 class="text-2xl font-bold mb-4">新規作成</h1>
            
            <form @submit.prevent="submit">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
                        件名
                    </label>
                    <input 
                        id="title"
                        v-model="form.title"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{ 'border-red-500': errors.title }"
                        type="text"
                        placeholder="件名を入力してください"
                    >
                    <div v-if="errors.title" class="text-red-500 text-xs italic">{{ errors.title }}</div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="content">
                        本文
                    </label>
                    <textarea 
                        id="content"
                        v-model="form.content"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{ 'border-red-500': errors.content }"
                        rows="4"
                        placeholder="本文を入力してください"
                    ></textarea>
                    <div v-if="errors.content" class="text-red-500 text-xs italic">{{ errors.content }}</div>
                </div>
                
                <div class="flex items-center justify-between">
                    <button 
                        type="submit" 
                        :disabled="form.processing"
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                        :class="{ 'opacity-50': form.processing }"
                    >
                        {{ form.processing ? '送信中...' : '送信' }}
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>