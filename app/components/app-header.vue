<template>
    <header class="flex justify-between items-center mt-10">
        <NuxtLink to="/" class="text-xl font-bold">
            Finance Tracker
        </NuxtLink>
        <UAvatar src="https://avatars.githubusercontent.com/u/739984?v=4" alt="Avatar" />
    </header>
</template>

<script setup>
const user = useSupabaseUser();

watch(user, (user) => {
    if (user) {
        console.log(user)
    }
}, { immediate: true })

</script>