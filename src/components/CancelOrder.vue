<!--
  Объект со списком причин отказа от заказа расположен в reasonsList. На его основе формируется верстка через v-for.
  Кнопка "Отправить" вызывает функцию submit.
  Выбранные причины собираются в массив selectedReasons.

  Функциональность:
  - Отображает список причин отказа с чекбоксами
  - По умолчанию выбран пункт "Не подходит тоннаж груза"
  - При нажатии кнопки "Отправить" собирает выбранные причины
-->

<template>
  <div class="cancel-order">
    <h3 class="cancel-order-title">Расскажите, почему отказались от выполнения заказа?</h3>
    
    <div class="options-list">
      <label v-for="(label, key) in reasonsList" :key="key" class="option-item">
        <input type="checkbox" v-model="reasons[key]" />
        <span class="option-text">{{ label }}</span>
      </label>
    </div>
    
    <button class="submit-button" @click="submit">Отправить</button>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const emit = defineEmits(['submit']);

const reasonsList = {
  date: 'Не подходит дата или время',
  tonnage: 'Не подходит тоннаж груза',
  volume: 'Не подходит объем груза',
  truckType: 'Не подходит тип фургона',
  noPass: 'Нет пропуска в МКАД ТТК СК',
  breakdown: 'Поломка машины/авария',
  sick: 'Заболел',
  noSanitary: 'Нет санобработки',
  noMedical: 'Нет мед. книжки',
  noDrivers: 'Нет гидроборта',
  noPlants: 'Нет растентовки',
  badRate: 'Не устраивает ставка за рейс',
  badRoute: 'Не устраивает маршрут',
  other: 'Другое'
};

const reasons = reactive(
  Object.keys(reasonsList).reduce((acc, key) => {
    acc[key] = key === 'tonnage';
    return acc;
  }, {})
);

const submit = () => {
  const selectedReasons = Object.entries(reasons)
    .filter(([_, value]) => value)
    .map(([key]) => key);
  
  if (selectedReasons.length === 0) {
    console.log('Пожалуйста, выберите хотя бы одну причину');
    return;
  }
  
  console.log('Выбранные причины:', selectedReasons);
  emit('submit', selectedReasons);
};
</script>

<style scoped>
.cancel-order {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.cancel-order-title {
  font-size: 16px;
  font-weight: bold;
  margin: 0;
  margin-top: 15px;
  text-align: center;
  color: #333;
  text-transform: uppercase;
}

.options-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-height: 400px;
  overflow-y: auto;

  scrollbar-width: thin;
  scrollbar-color:rgb(134, 134, 134) #D9D9D9;
}

.option-item {
  display: flex;
  gap: 12px;
  align-items: center;
  cursor: pointer;
  justify-content: center;
  padding: 0 15px;
}

.option-item input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #58595b;
  border-radius: 6px;
  position: relative;
  cursor: pointer;
}

.option-item input[type="checkbox"]:checked {
  background-color: transparent;
  border-color: #58595b;
}

.option-item input[type="checkbox"]:checked::before {
  content: '';
  position: absolute;
  top: 2px;
  left: 2px;
  right: 2px;
  bottom: 2px;
  background-color: #CD10FF;
  border-radius: 3px;
}

.option-text {
  font-size: 14px;
  color: #333;
  text-transform: uppercase;
  text-align: left;
  flex: 1;
  max-width: 280px;
}

.submit-button {
  background-color: white;
  color: black;
  border: 1px solid #CD10FF;
  border-radius: 8px;
  padding: 10px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s;
  text-transform: uppercase;
}

.submit-button:hover {
  background-color: #CD10FF;
  color: white;
}

.options-list::-webkit-scrollbar {
  width: 8px; 
}

.options-list::-webkit-scrollbar-track {
  background: #D9D9D9; 
  border-radius: 4px;
}

.options-list::-webkit-scrollbar-thumb {
  background-color: #D9D9D9;
  border-radius: 4px;
  border: 2px solid #D9D9D9;  
}

.options-list::-webkit-scrollbar-thumb:hover {   
  background-color: #D9D9D9;
}

</style> 