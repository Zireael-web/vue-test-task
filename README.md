Структура проекта:
<br>
Проект хранится в папке src.
<br>
папка components - для самих компонентов. Компоненты написаны на Vue 3 Composition API. Single-File Components подход, стили через scoped CSS
<br>
папка assets - для шрифтов и иконок

По поводу компонентов:
<br>
Было создана 2 компонента - Modal и CancelOrder, т к в ТЗ сказано что в пропс content можно передать VNode: то есть CancelOrder прокидывается в Modal
<br>
используется Single-File Components подход, стили через scoped CSS. Модальное окно выводим через Teleport. 
Перед template у каждого компонента прописан комментарий.

Запуск проекта:
<br>
npm install
<br>
npm run dev 
