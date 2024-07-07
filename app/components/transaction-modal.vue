<template>
    <UModal v-model="isOpen">
      <UCard>
        <template #header>
          Add Transaction
        </template>
  
        <UFormGroup label="Transaction Type" :required="true" name="Category" class="mb-4">
            <USelect type="transactionsType" :options="transactionsType" placeholder="Select Transaction Type"/>
        </UFormGroup>

        <UFormGroup label="Amount" required="true" name="amount" class="mb-4">
            <UInput type="number" placeholder="Amount"/>
        </UFormGroup>

        <UFormGroup label="Transaction Date" required="true" name="created_at" class="mb-4">
            <UInput type="date" icon="i-heroicons-calendar-days-20-solid" />
        </UFormGroup>

        <UFormGroup label="Description" hint="Optional" name="description" class="mb-4">
            <UInput type="number" placeholder="Description"/>
        </UFormGroup>

        <UFormGroup label="Category" :required="true" name="Category" class="mb-4">
            <USelect type="categoryOptions" :options="categoriesOptions" placeholder="Description"/>
        </UFormGroup>

        <div class="flex justify-end">
            <UButton class="px-5" type="submit" color="black" variant="solid" label="Save"/>
        </div>
      </UCard>
    </UModal>
  </template>
  
<script setup>
import { categoriesOptions, transactionsType } from '~/constants'
const props = defineProps({
modelValue: Boolean
})
const emit = defineEmits(['update:modelValue'])
const isOpen = computed({
    get: () => props.modelValue,
    set: (value) => emit('update:modelValue', value)
})
</script>