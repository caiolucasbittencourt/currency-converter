<template>
  <header class="app-logo">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      class="icon icon-tabler icons-tabler-outline icon-tabler-arrows-right-left"
    >
      <path stroke="none" d="M0 0h24v24H0z" fill="none" />
      <path d="M21 17h-18l4 -4" />
      <path d="M7 7h14l-4 4" />
    </svg>
  </header>
</template>

<style scoped>
.app-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  color: #eee;
  animation: fadeIn 0.8s ease-out both;
}

.app-logo svg {
  width: 3.2rem;
  height: 3.2rem;
  stroke: #000;
  stroke-width: 2.5;
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
