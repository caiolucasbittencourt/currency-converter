<script setup>
import { ref, onMounted } from 'vue'
import TheHeader from './components/TheHeader.vue'
import ConversionForm from './components/ConversionForm.vue'
import ResultDisplay from './components/ResultDisplay.vue'

const exchangeRates = ref({})
const isLoading = ref(true)
const showResult = ref(false)
const result = ref({
  originalValue: '--',
  exchangeRate: '--',
  finalResult: '--'
})

const API_URL = "https://economia.awesomeapi.com.br/last/USD-BRL,EUR-BRL,GBP-BRL,JPY-BRL,ARS-BRL"

async function fetchExchangeRates() {
  isLoading.value = true
  try {
    const response = await fetch(API_URL)
    const data = await response.json()
    exchangeRates.value = {
      USD: parseFloat(data.USDBRL.bid),
      EUR: parseFloat(data.EURBRL.bid),
      GBP: parseFloat(data.GBPBRL.bid),
      JPY: parseFloat(data.JPYBRL.bid),
      ARS: parseFloat(data.ARSBRL.bid),
    }
  } catch (error) {
    console.error("Falha ao buscar cotações:", error)
    alert("Não foi possível carregar as cotações.")
  } finally {
    isLoading.value = false
  }
}

function formatCurrency(value, currency) {
  return value.toLocaleString("pt-BR", {
    style: "currency",
    currency: currency,
    maximumFractionDigits: 2,
  })
}

function handleConversion(payload) {
  const { amount, currency } = payload
  const amountValue = parseFloat(amount)
  
  const rate = exchangeRates.value[currency]
  if (!rate) {
    alert("A cotação para a moeda selecionada não foi encontrada.")
    return
  }

  const convertedValue = amountValue * rate

  result.value = {
    originalValue: formatCurrency(amountValue, currency),
    exchangeRate: formatCurrency(rate, "BRL"),
    finalResult: formatCurrency(convertedValue, "BRL"),
  }

  showResult.value = true
}

onMounted(fetchExchangeRates)
</script>

<template>
  <TheHeader />

  <main>
    <ConversionForm :isLoading="isLoading" @convert="handleConversion" />

    <ResultDisplay v-if="showResult" :resultData="result" />
  </main>
</template>

<style scoped>
main {
  animation: fadeIn 0.8s ease-out both;
  animation-delay: 0.2s;
  width: 480px;
  border-radius: 0;
  border: 1px solid #222;
  background-color: #000000;
  overflow: hidden;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>