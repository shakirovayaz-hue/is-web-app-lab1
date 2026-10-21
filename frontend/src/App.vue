<script setup>
import { ref } from 'vue'

const currentScreen = ref('list')

const items = ref([
  { id: 1, number: 'REQ-2026-001', title: 'Поездка в аэропорт', carId: 3, status: 'New' },
  { id: 2, number: 'REQ-2026-002', title: 'Доставка документов в офис', carId: 1, status: 'InProgress' }
])
</script>

<template>
  <div class="app-container">
    <header>
      <h1>Гаражная служба: Заявки на авто</h1>
      <nav>
        <button type="button" @click="currentScreen = 'list'">Список заявок</button>
        <button type="button" @click="currentScreen = 'new'">Создать заявку</button>
        <button type="button" @click="currentScreen = 'login'">Вход</button>
      </nav>
    </header>

    <!-- ЭКРАН 1: Список -->
    <main v-if="currentScreen === 'list'">
      <h2>Список заявок</h2>
      <table>
        <thead>
          <tr>
            <th>Номер</th>
            <th>Тема</th>
            <th>Авто (ID)</th>
            <th>Статус</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>{{ item.number }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.carId }}</td>
            <td>{{ item.status }}</td>
          </tr>
        </tbody>
      </table>
    </main>

    <!-- ЭКРАН 2: Создание -->
    <main v-else-if="currentScreen === 'new'">
      <h2>Создание новой заявки</h2>
      <form @submit.prevent>
        <div class="form-group">
          <label for="title">Тема (5–80 символов)</label>
          <input id="title" name="title" type="text" autofocus required />
        </div>

        <div class="form-group">
          <label for="carId">ID автомобиля из справочника</label>
          <input id="carId" name="carId" type="number" min="1" required />
        </div>

        <div class="form-group">
          <label for="description">Описание (10–500 символов)</label>
          <textarea id="description" name="description" rows="4" required></textarea>
        </div>

        <button type="submit">Создать</button>
      </form>
    </main>

    <!-- ЭКРАН 3: Вход -->
    <main v-else-if="currentScreen === 'login'">
      <h2>Вход в систему</h2>
      <form @submit.prevent>
        <div class="form-group">
          <label for="login">Логин</label>
          <input id="login" name="login" type="text" autofocus required />
        </div>

        <div class="form-group">
          <label for="password">Пароль</label>
          <input id="password" name="password" type="password" required />
        </div>

        <button type="submit">Войти</button>
      </form>
    </main>
  </div>
</template>

<style scoped>
.app-container {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
header {
  margin-bottom: 20px;
  border-bottom: 2px solid #ccc;
  padding-bottom: 10px;
}
nav button {
  margin-right: 10px;
  padding: 8px 16px;
  cursor: pointer;
}
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}
th {
  background-color: #f4f4f4;
}
.form-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}
input, textarea {
  width: 100%;
  max-width: 400px;
  padding: 8px;
  box-sizing: border-box;
}
button[type="submit"] {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
button[type="submit"]:hover {
  background-color: #0056b3;
}
</style>