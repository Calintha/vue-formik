
<template>
    <input type="checkbox" :checked="modelValue" @input="$emit('update:modelValue', $event.target.checked);$event.stopPropagation()" />
</template>

<script setup>
const props = defineProps({
    modelValue: {
        type: Boolean,
        required: true
    }
})
console.log(props.modelValue)
</script>
