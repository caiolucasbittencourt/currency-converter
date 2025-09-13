<script setup>
defineProps({
  resultData: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <footer class="result-container show-result">
    <div class="result-row">
      <span>Valor original</span>
      <strong>{{ resultData.originalValue }}</strong>
    </div>

    <div class="result-row">
      <span>Cotação do dia</span>
      <strong>{{ resultData.exchangeRate }}</strong>
    </div>

    <div class="result-final">
      <span>Resultado em Reais</span>
      <h2>{{ resultData.finalResult }}</h2>
    </div>
  </footer>
</template>

<style scoped>
.result-container {
  padding: 0 3.5rem;
  width: 100%;
  transition: opacity 0.4s ease-in-out, padding 0.6s ease-in-out;
  padding: 2rem 3.5rem;
}
.show-result {
  opacity: 1;
}
.result-row, .result-final {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding-bottom: 1rem;
  margin-bottom: 1rem;
  border-bottom: 1px solid #222;
}
.result-final {
  border-bottom: none;
  margin-bottom: 0;
}
.result-container span {
  color: #888;
  font-size: 0.9rem;
}
.result-row strong {
  color: #f0f0f0;
  font-family: "IBM Plex Mono", monospace;
  font-size: 1.1rem;
}
.result-final h2 {
  color: #ffffff;
  font-weight: 700;
  font-size: 2.2rem;
  line-height: 1;
}
</style>