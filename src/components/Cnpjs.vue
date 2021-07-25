<template>
  <div class="container">
    <h3> CNPJ:</h3>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">City</th>
        </tr>
      </thead>
      <tbody>
        {{cnpjs}}
        <tr> 
          <th scope="row">{{cnpjs.nome}}</th>
          <td>{{cnpjs.uf}}</td>
          <td>{{cnpjs.uf}}</td>
          <td>{{cnpjs.atividade_principal.text}}</td>
        </tr>
      </tbody>
    </table> 
  </div> 
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Cnpjs',
    data() {
      return {
        cnpjs: null,
      };
    },
    created: function() {
      axios
        .post('https://cerberusus.herokuapp.com/api', { cnpj: '14707364000110'})
        .then(res => {
          this.cnpjs = res.data;
        })
    }
  }
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>