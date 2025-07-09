<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
    <input :value="modelValue" @input="$emit('update:modelValue',$event.target.value)" v-bind="$attrs" class="flex-1 bg-gray-800 text-white border border-gray-600 rounded p-2" />
</template>
