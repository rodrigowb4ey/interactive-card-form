<script setup lang="ts">
import { ref, computed } from 'vue';

type CardForm = {
  name: string;
  cardNumber: string;
  expDateMonth: string;
  expDateYear: string;
  cvc: string;
}

const cardForm = ref<CardForm>({
  name: '',
  cardNumber: '',
  expDateMonth: '',
  expDateYear: '',
  cvc: '',
});

const submitForm = (formData: CardForm) => {
  console.log('Form submitted:', formData);
};

const formatCardNumber = (event: Event) => {
  const inputElement = event.target as HTMLInputElement | null;
  if (inputElement) {
    const value = inputElement.value;
    const cleanedValue = value.replace(/\D/g, '');
    const formattedValue = cleanedValue.replace(/(\d{4})/g, '$1 ').trim();
    cardForm.value.cardNumber = formattedValue;
  }
};

const formatExpDateMonthNumber = (event: Event) => {
  const inputElement = event.target as HTMLInputElement | null;
  if (inputElement) {
    const value = inputElement.value;
    const cleanedValue = value.replace(/\D/g, '');
    cardForm.value.expDateMonth = cleanedValue
  }
};

const formatExpDateYearNumber = (event: Event) => {
  const inputElement = event.target as HTMLInputElement | null;
  if (inputElement) {
    const value = inputElement.value;
    const cleanedValue = value.replace(/\D/g, '');
    cardForm.value.expDateYear = cleanedValue
  }
};

const formatCvcNumber = (event: Event) => {
  const inputElement = event.target as HTMLInputElement | null;
  if (inputElement) {
    const value = inputElement.value;
    const cleanedValue = value.replace(/\D/g, '');
    cardForm.value.cvc = cleanedValue
  }
};

const formattedDateDisplay = computed(() => {
  if (!cardForm.value.expDateMonth && !cardForm.value.expDateYear) {
    return '00/00'
  };

  return `${cardForm.value.expDateMonth}/${cardForm.value.expDateYear}`;
});
</script>

<template>
  <main class="flex">
    <section
      id="card-faces"
      class="flex flex-col justify-around place-items-center h-full w-1/2 gap-12"
    >
      <div class="flex h-1/2 w-full items-end justify-start" id="card-front">
        <div class="relative ml-24" id="card-front-img">
          <img
            class="h-fit w-fit"
            src="/assets/images/bg-card-front.png"
            alt="Card Front"
          />
          <img
            class="absolute h-fit w-fit top-4 left-6"
            src="/assets/images/card-logo.svg"
          />
          <span
            class="text-white text-2xl absolute font-light bottom-16 left-6"
          >
            {{ cardForm.cardNumber ? cardForm.cardNumber :  '0000 0000 0000 0000'}}
          </span>
          <span class="text-white absolute font-light text-sm bottom-4 left-6">
            {{ cardForm.name.toUpperCase() }}
          </span>
          <span class="text-white absolute font-light text-sm bottom-4 right-6">
            {{ formattedDateDisplay }}
          </span>
        </div>
      </div>
      <div class="flex h-1/2 w-full items-start justify-end" id="card-back">
        <div class="relative mr-24" id="card-back-img">
          <img
            class="h-fit w-fit"
            src="/assets/images/bg-card-back.png"
            alt="Card Back"
          />
          <span class="text-white text-sm absolute font-light top-24 right-12">
            {{ cardForm.cvc ? cardForm.cvc : '000' }}
          </span>
        </div>
      </div>
    </section>
    <section
      id="card-form"
      class="flex flex-col justify-around place-items-center h-full w-1/2"
    >
      <form
        @submit.prevent="submitForm(cardForm)"
        class="flex flex-col gap-6 items-center justify-center h-5/6 w-3/4 text-[#21092f]"
      >
        <section class="flex flex-col w-4/5 gap-1" id="card-field-name">
          <label for="card-name">CARDHOLDER NAME</label>
          <input
            id="card-name"
            class="border-2 border-[#dedddf] rounded-md py-2 px-2"
            v-model="cardForm.name"
            placeholder="e.g. Jane Appleseed"
          />
        </section>
        <section class="flex flex-col w-4/5 gap-1" id="card-field-number">
          <label for="card-number">CARD NUMBER</label>
          <input
            id="card-number"
            class="border-2 border-[#dedddf] rounded-md py-2 px-2"
            v-model="cardForm.cardNumber"
            @input="formatCardNumber"
            maxlength="19"
            placeholder="e.g. 1234 5678 9123 0000"
          />
        </section>
        <div class="flex flex-row w-4/5 gap-4">
          <section class="flex flex-col w-1/2 gap-1" id="card-field-exp-date">
            <label for="card-exp-date">EXP. DATE (MM/YY)</label>
            <div class="flex gap-2">
              <input
                class="border-2 border-[#dedddf] rounded-md w-3/5 px-3 py-2"
                id="card-exp-date-month"
                v-model="cardForm.expDateMonth"
                @input="formatExpDateMonthNumber"
                maxlength="2"
                placeholder="MM"
              />
              <input
                class="border-2 border-[#dedddf] rounded-md w-3/5 px-3 py-2"
                id="card-exp-date-year"
                v-model="cardForm.expDateYear"
                @input="formatExpDateYearNumber"
                maxlength="2"
                placeholder="YY"
              />
            </div>
          </section>
          <section class="flex flex-col w-1/2 gap-1" id="card-field-cvc">
            <label for="card-cvc">CVC</label>
            <input
              class="border-2 border-[#dedddf] rounded-md py-2 px-3"
              id="card-cvc"
              v-model="cardForm.cvc"
              @input="formatCvcNumber"
              maxlength="3"
              placeholder="e.g. 123"
            />
          </section>
        </div>
        <button
          class="w-4/5 py-4 mt-8 border-2 rounded-md bg-[#21092f] text-white"
          type="submit"
        >
          Confirm
        </button>
      </form>
    </section>
  </main>
</template>

<style scoped></style>
