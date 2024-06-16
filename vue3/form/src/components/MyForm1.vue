<template>
  <BForm @submit="onSubmit">
    <BFormGroup
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
    >
      <BFormInput
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
      />
      <BFormInvalidFeedback :state="formValid.email">
        please enter your email
      </BFormInvalidFeedback>
    </BFormGroup>

    <BFormGroup id="input-group-2" label="Your Name:" label-for="input-2">
      <BFormInput id="input-2" v-model="form.name" placeholder="Enter name"/>
      <BFormInvalidFeedback :state="formValid.name">
        please enter your name
      </BFormInvalidFeedback>
    </BFormGroup>

    <BFormGroup id="input-group-3" label="Food:" label-for="input-3">
      <BFormSelect id="input-3" v-model="form.food" :options="foods"/>
      <BFormInvalidFeedback :state="formValid.food">
        please select food
      </BFormInvalidFeedback>
    </BFormGroup>

    <BFormGroup id="input-group-4">
      <BFormCheckboxGroup v-model="form.checked" id="checkboxes-4">
        <BFormCheckbox value="me">Check me out</BFormCheckbox>
        <BFormCheckbox value="that">Check that out</BFormCheckbox>
      </BFormCheckboxGroup>
      <BFormInvalidFeedback :state="formValid.checked">
        please check at least one
      </BFormInvalidFeedback>
    </BFormGroup>

    <BButton class="mt-5" type="submit" variant="primary">Submit</BButton>
  </BForm>
</template>

<script setup>
import {reactive, computed} from "vue";
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

const foods = [{text: 'Select One', value: null}, 'Carrots', 'Beans', 'Tomatoes', 'Corn'];
const form = reactive({
  email: '',
  name: '',
  food: null,
  checked: [],
});

const formValid = reactive({
  email: false,
  name: false,
  food: false,
  checked: false,
});

// 方法二 使用computed
// const isEmailValid = computed(() => form.email.length > 0);
// const isNameValid = computed(() => form.name.length > 0);
// const isFoodValid = computed(() => form.food !== null);
// const isCheckedValid = computed(() => form.checked.length > 0);

// 優化：如何第一次進入頁面就不顯示錯誤訊息，等實際輸入了再做判斷

const onSubmit = (event) => {
  event.preventDefault();

  // 方法一 使用reactive
  formValid.email = form.email.length > 0;
  formValid.name = form.name.length > 0;
  formValid.food = form.food !== null;
  formValid.checked = form.checked.length > 0;

  console.log(JSON.stringify(form))
};
</script>

<style scoped>

</style>