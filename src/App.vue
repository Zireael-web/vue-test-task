<template>
  <div class="app">
    <button @click="openModal" class="open-button">Открыть модальное окно</button>
    
    <Modal 
      :isOpen="isModalOpen" 
      :onClose="closeModal" 
      title="Отказаться от выполнения заказа"
      orderNumber="№ У00017711"
      :content="CancelOrder"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from './components/Modal.vue';
import CancelOrder from './components/CancelOrder.vue';

const isModalOpen = ref(false);

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};
</script>

<style scoped>
.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

h1 {
  margin-bottom: 2rem;
  color: #333;
}

.open-button {
  background-color: #9c27b0;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.open-button:hover {
  background-color: #7b1fa2;
}
</style>
