<template>
    <UModal v-model="isOpen">
        <UCard>
            <template #header>
                Add Transaction
            </template>
            <UFormGroup label="Transaction Type" :schema="schema" ref="form" @submit.prevent="save" :required="true"
                name="Category" class="mb-4">
                <USelect :options="transactionsType" placeholder="Select Transaction Type" v-model="state.type" />
            </UFormGroup>

            <UFormGroup label="Amount" :required="true" name="amount" class="mb-4">
                <UInput type="number" placeholder="Amount" v-model.number="state.amount" />
            </UFormGroup>

            <UFormGroup label="Transaction Date" :required="true" name="created_at" class="mb-4">
                <UInput type="date" icon="i-heroicons-calendar-days-20-solid" v-model="state.created_at" />
            </UFormGroup>

            <UFormGroup label="Description" hint="Optional" name="description" class="mb-4">
                <UInput placeholder="Description" v-model="state.description" />
            </UFormGroup>

            <UFormGroup label="Category" :required="true" name="Category" class="mb-4" v-if="state.type === 'Expense'">
                <USelect :options="categoriesOptions" placeholder="Description" v-model="state.category" />
            </UFormGroup>

            <div class="flex justify-end">
                <UButton class="px-5" type="submit" color="black" variant="solid" label="Save" />
            </div>
        </UCard>
    </UModal>
</template>

<script setup>
import { categoriesOptions, transactionsType } from '~/constants'
import { z } from 'zod'
const props = defineProps({
    modelValue: Boolean
})
const emit = defineEmits(['update:modelValue'])

const defaultSchema = z.object({
    created_at: z.string(),
    description: z.string().optional(),
    amount: z.number().positive('Amount needs to be more than 0')
})

const incomeSchema = z.object({
    type: z.literal("Income")
})

const expenseSchema = z.object({
    type: z.literal("Expense"),
    category: z.enum(categoriesOptions)
})

const investmentSchema = z.object({
    type: z.literal("Investment")
})

const savingSchema = z.object({
    type: z.literal('Saving')
})

const schema = z.intersection(
    z.discriminatedUnion('type', [incomeSchema, expenseSchema, investmentSchema, savingSchema]),
    defaultSchema
)

const form = ref()

const save = async () => {
    form.value.validate()
}

const isOpen = computed({
    get: () => props.modelValue,
    set: (value) => emit('update:modelValue', value)
})

const state = ref({
    type: undefined,
    amount: 0,
    created_at: undefined,
    description: undefined,
    category: undefined
})
</script>