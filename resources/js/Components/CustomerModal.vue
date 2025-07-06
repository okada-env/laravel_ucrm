<script setup>
import { ref, onMounted, computed } from 'vue'
import Modal from '@/Components/Modal.vue'
import { Inertia } from '@inertiajs/inertia'

const props = defineProps({
    show: {
        type: Boolean,
        default: false,
    }
})

const emit = defineEmits(['close', 'update:customerId'])

const customers = ref([])
const searchQuery = ref('')
const selectedCustomer = ref(null)

onMounted(async () => {
    // 会員データを取得
    try {
        const response = await fetch('/api/customers')
        const data = await response.json()
        customers.value = data
    } catch (error) {
        console.error('会員データの取得に失敗しました:', error)
    }
})

const filteredCustomers = computed(() => {
    if (!searchQuery.value) return customers.value
    return customers.value.filter(customer => 
        customer.name.includes(searchQuery.value) || 
        customer.kana.includes(searchQuery.value)
    )
})

const selectCustomer = (customer) => {
    selectedCustomer.value = customer
    emit('update:customerId', customer.id)
    emit('close')
}

const closeModal = () => {
    emit('close')
}
</script>

<template>
    <Modal :show="show" @close="closeModal">
        <div class="p-6">
            <h3 class="text-lg font-medium text-gray-900 mb-4">会員を選択</h3>
            
            <div class="mb-4">
                <input
                    type="text"
                    v-model="searchQuery"
                    placeholder="会員名で検索..."
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
                >
            </div>
            
            <div class="max-h-60 overflow-y-auto">
                <div
                    v-for="customer in filteredCustomers"
                    :key="customer.id"
                    @click="selectCustomer(customer)"
                    class="p-3 border-b border-gray-200 hover:bg-gray-50 cursor-pointer"
                >
                    <div class="font-medium">{{ customer.name }}</div>
                    <div class="text-sm text-gray-600">{{ customer.kana }}</div>
                </div>
            </div>
            
            <div class="mt-4 flex justify-end">
                <button
                    @click="closeModal"
                    class="px-4 py-2 text-sm font-medium text-gray-700 bg-gray-200 rounded-md hover:bg-gray-300"
                >
                    キャンセル
                </button>
            </div>
        </div>
    </Modal>
</template> 