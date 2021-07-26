<template id="consulta">
  <div class="container">
    <h1> WeDecode CNPJ</h1>
    <div id="form">
      <form @submit="getInfo" onsubmit="return false">
        <label for="cnpj">Digite um CNPJ</label>
        <input type="text" id="cnpj" minlength="14" maxlength="18" name="cnpj" placeholder="14707364000110"/>
        <button type="submit">Consultar</button>
      </form>
    </div>
    <nav v-if="wide == 14" v-cloak>
      <li>
        <span> Informações </span>
        <ul>{{cnpjs["NOME FANTASIA"]}} {{cnpjs["STATUS"]}}</ul>
        <ul>{{"Razão Social: " +cnpjs["RAZAO SOCIAL"]}}</ul>
        <ul>{{cnpjs["CNAE PRINCIPAL DESCRICAO"]}}</ul>
        <ul>{{cnpjs["TIPO LOGRADOURO"]}} {{cnpjs["LOGRADOURO"]}} {{cnpjs["BAIRRO"]}}- {{cnpjs["MUNICIPIO"]}} {{cnpjs["UF"]}} - {{cnpjs["CEP"]}}</ul>
        <ul>{{"Desde: " + cnpjs["DATA ABERTURA"]}}</ul>
        <ul>{{"Cnpj: " +cnpjs["CNPJ"]}}</ul>
        <ul>{{"Complemento: " +cnpjs["COMPLEMENTO"]}}</ul>
        <ul>{{"Telefone: " +cnpjs["DDD"]}} {{cnpjs["TELEFONE"]}}</ul>
        <ul>{{"Cnae: " +cnpjs["CNAE PRINCIPAL CODIGO"]}}</ul>
        <ul>{{"Email: " +cnpjs["EMAIL"]}}</ul>
      </li>
    </nav>
  </div> 
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Cnpjs',
    data() {
      return {
        cnpjs: [],
        cnpj: 0,
        wide: 0,
      };
    },
    methods: {
      getInfo: function() {
        let cnpj = document.getElementById('cnpj').value
        axios
          .get(`https://api-publica.speedio.com.br/buscarcnpj?cnpj=${cnpj}`)
          .then(res => {
              this.cnpjs = res.data;
              this.cnpj = cnpj;
              this.wide = cnpj.length;
          }).catch(error => {
            console.log('Error: ', error)
          })
      }
    }
  }
</script>

<style>
  :root {
    --clr-background: #eceff1;
    --clr-white: #ffffff;
    --clr-primary: #aaffaa;
    --clr-gray: #263238;
    --font-size: 16px;
    --border-radius: 0.2em;
  }
  h3 {
    margin-bottom: 5%;
  }
  body {
    background-color: var(--clr-background);
  }
  form {
    display: grid;
    gap:  10px;
  }
  button {
    border-radius: var(--border-radius);
    border: 1px solid var(--clr-gray);
    background-color: var(--clr-primary);
  }
  input {
    border-radius: var(--border-radius); 
    border: 1px solid var(--clr-gray);
  }
  nav {
    margin-top: 10px;
    border: 1px solid var(--clr-gray);
    border-radius: var(--border-radius);
    background-color: var(--clr-gray);
    color: var(--clr-white);
  }
  li {
    list-style: none;
  }
  [v-cloak] {
    display: none;
  }
</style>