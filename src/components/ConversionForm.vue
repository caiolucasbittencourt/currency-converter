<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  isLoading: {
    type: Boolean,
    required: true
  }
})

const amount = ref('')
const selectedCurrency = ref('')

const emit = defineEmits(['convert'])

function handleSubmit() {
  if (!amount.value || !selectedCurrency.value) {
    alert("Por favor, preencha o valor e selecione uma moeda.")
    return;
  }
  emit('convert', { 
    amount: String(amount.value).replace(',', '.'), 
    currency: selectedCurrency.value 
  })
}

const buttonText = computed(() => {
  return props.isLoading ? "Carregando cotações..." : "Converter em reais"
})
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <label for="amount">valor</label>
    <input v-model="amount" type="text" id="amount" placeholder="0" required />

    <label for="currency">moeda</label>
    <select v-model="selectedCurrency" id="currency" required>
      <option value="" disabled selected hidden>Selecione a moeda</option>
      <option value="USD">Dólar Americano</option>
      <option value="EUR">Euro</option>
      <option value="GBP">Libra Esterlina</option>
      <option value="JPY">Iene Japonês</option>
      <option value="ARS">Peso Argentino</option>
    </select>
    
    <button type="submit" :disabled="isLoading">{{ buttonText }}</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  padding: 3rem 3.5rem;
}
label {
  font-size: 0.7rem;
  color: #888;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 0.5rem;
  margin-top: 1.5rem;
}
input, select {
  outline: 0;
  color: #f0f0f0;
  background-color: transparent;
  padding: 0.75rem 0.25rem;
  font-family: "Inter", sans-serif;
  font-size: 1.25rem;
  border: none;
  border-radius: 0;
  border-bottom: 2px solid #333;
  transition: border-color 0.3s ease;
}
select {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill='none' stroke='%23888' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='m2 5 6 6 6-6'/%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right 0.25rem center;
  background-size: 1em;
  cursor: pointer;
}
option {
  background-color: #1a1a1a;
}
input::placeholder, select:invalid {
  color: #555;
}
input:focus, select:focus {
  border-bottom-color: #f5f5f5;
}
button {
  height: 3.25rem;
  background: #f5f5f5;
  color: #000;
  border: none;
  border-radius: 0;
  font-family: "Inter", sans-serif;
  font-size: 1rem;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  cursor: pointer;
  margin-top: 3rem;
  outline: 0;
  transition: background-color 0.2s ease, transform 0.2s ease;
}
button:hover {
  background: #ffffff;
  transform: scale(1.05);
}
button:disabled {
  background-color: #222;
  color: #555;
  cursor: not-allowed;
  transform: scale(1);
}
</style>