<template>
    <component v-if="typeof as === 'string'" :is="as" :value="formik.values[name]" @input="formik.setValues(name, $event.target.value)" @update:modelValue="value => formik.setValues(name, value)"></component>
    <component v-else :is="as" :value="formik.values[name]" :modelValue="formik.values[name]" @update:modelValue="value => formik.setValues(name, value)"></component>
</template>

<script setup>
import { inject } from 'vue'
const formik = inject('formik')

const emit = defineEmits(['update:value'])

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    as: {
        type: String,
        default: 'input'
    },
})

console.log(formik.values)
console.log(props.name)
</script>