<template>
  <BContainer class="p-3">
    <BRow>
      <BCol>
<!--        <MyForm1/>-->
          <MyForm2 />
      </BCol>
    </BRow>
  </BContainer>
</template>

<script setup>
import {BContainer, BRow, BCol, BButton, BCardText} from "bootstrap-vue-next";
import MyForm1 from "@/components/MyForm1.vue";
import MyForm2 from "@/components/MyForm2.vue";

</script>

<style>
</style>

