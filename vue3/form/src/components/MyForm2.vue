<template>
    <BForm @submit="onSubmit">
      <BFormGroup
          id="input-group-1"
          label="Email address:"
          label-for="input-1"
      >
        <BFormInput
            id="input-1"
            v-model="email"
            type="email"
            placeholder="Enter email"
        />
        <BFormInvalidFeedback :state="!errors.email">
          {{ errors.email }}
        </BFormInvalidFeedback>
      </BFormGroup>
  
      <BFormGroup id="input-group-2" label="Your Name:" label-for="input-2">
        <BFormInput id="input-2" v-model="name" placeholder="Enter name"/>
        <BFormInvalidFeedback :state="!errors.name">
          {{ errors.name }}
        </BFormInvalidFeedback>
      </BFormGroup>
  
      <BFormGroup id="input-group-3" label="Food:" label-for="input-3">
        <BFormSelect id="input-3" v-model="food" :options="foods"/>
        <BFormInvalidFeedback :state="!errors.food">
          {{ errors.food }}
        </BFormInvalidFeedback>
      </BFormGroup>
  
      <BFormGroup id="input-group-4">
        <BFormCheckboxGroup v-model="checked" id="checkboxes-4">
          <BFormCheckbox value="me">Check me out</BFormCheckbox>
          <BFormCheckbox value="that">Check that out</BFormCheckbox>
        </BFormCheckboxGroup>
        <BFormInvalidFeedback :state="!errors.checked">
          {{ errors.checked }}
        </BFormInvalidFeedback>
      </BFormGroup>
  
      <BButton class="mt-5" type="submit" variant="primary">Submit</BButton>
      <BButton class="mt-5 mx-1" variant="danger" @click="onReset()">Reset
      </BButton>
    </BForm>
  </template>
  
  <script setup>
  import {
    BForm,
    BFormGroup,
    BFormInput,
    BFormCheckboxGroup,
    BFormCheckbox,
    BFormSelect,
    BButton,
    BFormInvalidFeedback
  } from "bootstrap-vue-next";
  import {useForm} from "vee-validate";
  import * as yup from "yup";
  
  const foods = [{text: 'Select One', value: null}, 'Carrots', 'Beans', 'Tomatoes', 'Corn'];
  
  const initialValues = {
    email: '',
    name: 'Tom',
    food: null,
    checked: [],
  };
  
  
  const validationSchema = yup.object({
    email: yup.string().required("please enter your email"),
    name: yup.string().required("please enter your name"),
    food: yup.string().required("please select food"),
    checked: yup.array().min(1, "please check at least one")
  });
  
  const {resetForm, handleSubmit, defineField, errors} = useForm({
    validationSchema,
    initialValues
  });
  
  const [email] = defineField('email')
  const [name] = defineField('name')
  const [food] = defineField('food')
  const [checked] = defineField('checked')
  
  const onSubmit = handleSubmit((values) => {
    console.log('Form Submitted', values);
  });
  
  const onReset = () => resetForm({values: initialValues});
  
  </script>
  
  <style scoped>
  
  </style>