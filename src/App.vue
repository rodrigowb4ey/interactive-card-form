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
  <main class="flex">
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
      <form @submit.prevent="submitForm(cardForm)" class="flex flex-col gap-6 items-center justify-center h-5/6 w-3/4 text-[#21092f]">
        <section class="flex flex-col w-4/5 gap-1" id="card-field-name">
          <label for="card-name">CARDHOLDER NAME</label>
          <input id="card-name" class="border-2 border-[#dedddf] rounded-md py-2 px-2" v-model="cardForm.name" placeholder="e.g. Jane Appleseed">
        </section>
        <section class="flex flex-col w-4/5 gap-1" id="card-field-number">
          <label for="card-number">CARD NUMBER</label>
          <input id="card-number" class="border-2 border-[#dedddf] rounded-md py-2 px-2" v-model="cardForm.cardNumber" placeholder="e.g. 1234 5678 9123 0000">
        </section>
        <div class="flex flex-row w-4/5 gap-4">
          <section class="flex flex-col w-1/2 gap-1" id="card-field-exp-date">
            <label for="card-exp-date">EXP. DATE (MM/YY)</label>
            <div class="flex gap-2">
              <input class="border-2 border-[#dedddf] rounded-md w-3/5 px-3 py-2" id="card-exp-date-month" v-model="cardForm.expDateMonth" placeholder="MM">
              <input class="border-2 border-[#dedddf] rounded-md w-3/5 px-3 py-2" id="card-exp-date-year" v-model="cardForm.expDateYear" placeholder="YY">
            </div>
          </section>        
          <section class="flex flex-col w-1/2 gap-1" id="card-field-cvc">
            <label for="card-cvc">CVC</label>
            <input class="border-2 border-[#dedddf] rounded-md py-2 px-3" id="card-cvc" v-model="cardForm.cvc">
          </section>
        </div>
        <button class="w-4/5 py-4 border-2 rounded-md bg-[#21092f] text-white" type="submit">Confirm</button>
      </form>
    </section>
  </main>
</template>

<style scoped>
</style>
