<template>
<div class="main container mt-5">
  <h1 class="text-center">Таблица с данными из API</h1>

  <div class="form-check form-switch">
    <input class="form-check-input" type="checkbox" id="switch1" @change="sortAlph" v-model="sortByAlph">
    <label class="form-check-label" for="switch1">Сортировка имени по алфавиту</label>
  </div>

  <div class="form-check form-switch">
    <input class="form-check-input" type="checkbox" id="switch2" @change="sortLen" v-model="sortByLen">
    <label class="form-check-label" for="switch2">Сортировка имени по длине</label>
  </div>

  <table class="table table-dark table-hover mt-3" id="table">
    <thead>
      <tr>
        <th><a href="#">ID</a></th>
        <th>Имя</th>
        <th>Фамилия</th>
        <th>Возраст</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in info" v-bind:key="user.id">
        <th scope="row">{{user.id}}</th>
        <td>{{user.firstName}}</td>
        <td>{{user.lastName}}</td>
        <td>{{user.age}}</td>
        <td>{{user.email}}</td>
      </tr>
    </tbody>
  </table>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      info: null,
    };
  },
  methods: {
    sortAlph() {
      this.info.sort((a, b) => {
        if (this.sortByAlph) {
          return (a.firstName.toLowerCase() > b.firstName.toLowerCase()) ? 1 : -1
        } else {
          return (a.firstName.toLowerCase() > b.firstName.toLowerCase()) ? -1 : 1
        }
      });
    },
    sortLen() {
      this.info.sort((a, b) => {
        if (this.sortByLen) {
          return (a.firstName.length > b.firstName.length) ? -1 : 1
        } else {
          return (b.firstName.length > a.firstName.length) ? -1 : 1
        }
      });
    },
  },
  mounted() {
    axios
      .get('http://vuetask.kih.ru/api.php')
      .then(response => (this.info = response.data));
  },
}
</script>
