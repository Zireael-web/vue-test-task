<!--
  Универсальный компонент модального окна.
  
  Принимает пропсы:
  - isOpen: булево значение, контролирующее видимость модального окна
  - onClose: функция, вызываемая при закрытии окна
  - title: заголовок модального окна
  - orderNumber: номер заказа, отображаемый жирным шрифтом
  - content: содержимое модального окна (строка HTML или Vue-компонент)

  Закрывается при клике на кнопку закрытия или на область вне окна.
  Использует Teleport для размещения в body.
-->
<template>
  <Teleport to="body">
    <div v-if="isOpen" class="modal-overlay" @click="handleOverlayClick">
      <div class="modal-container" @click.stop>
        <div class="modal-close">
          <button class="modal-close-button" @click="onClose">
            <img :src="closeIcon" alt="Close" width="24" height="24" />
          </button>
        </div>
        <div class="modal-header">
          <h2 class="modal-title">
            {{ title }} <span v-if="orderNumber" class="order-number">{{ orderNumber }}</span>
          </h2>
        </div>
        <div class="modal-content">
          <component :is="content" v-if="typeof content !== 'string'"></component>
          <div v-else v-html="content"></div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
import { defineProps } from 'vue';
import closeIcon from '../assets/icons/close.svg';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  onClose: {
    type: Function,
    required: true
  },
  title: {
    type: String,
    default: ''
  },
  orderNumber: {
    type: String,
    default: ''
  },
  content: {
    type: [String, Object],
    default: ''
  }
});

const handleOverlayClick = () => {
  props.onClose();
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-container {
  background-color: white;
  border-radius: 30px;
  width: 92%;
  max-width: 320px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  overflow: hidden;
  padding: 12px 24px 16px 24px;
}

.modal-close {
  width: 100%;
  display: flex;
  justify-content: flex-end;
}

.modal-header {
  text-align: center;
}

.modal-title {
  margin: 0;
  margin-top: 12px;
  text-transform: uppercase;
  font-size: 15px;
  font-weight: 400;
  color: #333;
  text-align: center;
}

.order-number {
  display: block;
  font-weight: 700;
}

.modal-close-button {
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style> 