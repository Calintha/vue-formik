<template>
  <Formik :initialValues="initialValues" :validate="onValidate" :onSubmit="onSubmit" v-slot="{formik, handleSubmit}">
    <form @submit.prevent="handleSubmit">
      <Field name="username"/>
      <Field name="age" type="number"/>
      <Field name="email"/>
      <Field name="password" type="password"/>
      <Field :as="Checkbox" name="hello"/>
      <button type="submit">Submit</button>
    </form>
  </Formik>
</template>

<script setup>
import Formik from './components/Formik.vue';
import Field from './components/Field.vue';
import Checkbox from './components/Checkbox.vue';

const onSubmit = (values) => {
  console.log(values);
};

let initialValues = {
  age: 23,
  username: 'Alexis',
  email: 'alexislours@protonmail.com',
  hello: true,
};

const onValidate = (values) => {
  const errors = {};

  if (!values.age) {
    errors.age = 'Required';
  } else if (values.age < 18) {
    errors.age = 'Must be 18 or older';
  }

  if (!values.username) {
    errors.username = 'Required';
  } else if (values.username.length < 3) {
    errors.username = 'Must be 3 characters or more';
  }

  if (!values.email) {
    errors.email = 'Required';
  } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)) {
    errors.email = 'Invalid email address';
  }

  return errors;
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
</style>
