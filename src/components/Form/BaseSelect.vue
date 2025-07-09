<script setup>
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue'])

</script>

<template>
    <select value="modelValue" @change="$emit('update:modelValue', $event.target.value)"
        class="w-full bg-gray-800 text-white border border-gray-600 rounded p-2">
        <slot />
    </select>
</template>
