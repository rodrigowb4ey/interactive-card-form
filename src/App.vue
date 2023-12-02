<script setup lang="ts">
import { ref } from 'vue';

interface CardForm {
  name: string;
  cardNumber: string;
  expDateMonth: number;
  expDateYear: number;
  cvc: number;
}

const cardForm = ref<CardForm>({
  name: '',
  cardNumber: '',
  expDateMonth: 0,
  expDateYear: 0,
  cvc: 0
});

const submitForm = (formData: CardForm) => {
  console.log('Form submitted:', formData);
};
</script>

<template>
  <main class="flex border-4 border-yellow-500">
    <section
      id="card-faces"
      class="flex flex-col justify-around place-items-center border-2 border-blue-700 h-full w-1/2"
    >
      <img
        class="flex h-fit w-fit pr-16"
        src="/assets/images/bg-card-front.png"
        alt="Card Front"
      />
      <img
        class="flex h-fit w-fit pr-16"
        src="/assets/images/bg-card-back.png"
        alt="Card Back"
      />
    </section>
    <section
      id="card-form"
      class="flex flex-col justify-around place-items-center border-2 border-red-700 h-full w-1/2"
    >
      <form @submit.prevent="() => submitForm(cardForm)" class="flex flex-col place-items-center border-2 border-green-700 h-5/6 w-3/4">
        <label for="card-name">CARDHOLDER NAME</label>
        <input id="card-name" v-model="cardForm.name" placeholder="e.g. Jane Appleseed">
        <label for="card-number">CARDHOLDER NUMBER</label>
        <input id="card-number" v-model="cardForm.cardNumber" placeholder="e.g. 1234 5678 9123 0000">
        <label for="card-exp-date">EXP. DATE (MM/YY)</label>
        <input id="card-exp-date-month" v-model="cardForm.expDateMonth">
        <input id="card-exp-date-year" v-model="cardForm.expDateYear">
        <label for="card-cvc">CVC</label>
        <input id="card-cvc" v-model="cardForm.cvc">
        <button type="submit">Confirm</button>
      </form>
    </section>
  </main>
</template>

<style scoped>
</style>
