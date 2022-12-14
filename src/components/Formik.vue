<template>
    <slot :values="values" @update:value="logValues" :handleSubmit="formSubmit"/>
</template>

<script setup>
import { provide, reactive } from 'vue';
const props = defineProps({
    onSubmit: {
        type: Function,
        required: true
    },
    initialValues: {
        type: Object,
        required: true
    },
    validate: {
        type: Function,
        required: true
    }
})

let initialValues = props.initialValues;

const state = reactive({
    values: initialValues,
    errors: {},
})

const formSubmit = () => {
    const errors = props.validate(state.values);
    if (Object.keys(state.errors).length === 0) {
        props.onSubmit(state.values);
    } else {
        state.setErrors(state.errors);
    }
}

provide('formik', {
    values: state.values,
    errors: state.errors,
    setValues: (name, value) => {
        console.log(name, value);
        state.values = {
            ...state.values,
            [name]: value
        };
    },
    setErrors: (errors) => {
        state.errors = errors;
    }
})
</script>