<template>
  <h3>Добавить новую транзакцию</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Количество <br />
        (отрицательно - расход, положительно - доход)</label
      >
      <input
        type="text"
        id="amount"
        placeholder="Введите количество..."
        v-model="amount"
      />
    </div>
    <button class="btn">Добавить транзакцию</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');

// Get toast interface
const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error('Оба поля должны быть обязательно заполнены!');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
};
</script>
