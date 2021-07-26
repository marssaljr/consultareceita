<template id="consulta">
  <div class="container">
    <div id="title">
      <h1>WeDecode CNPJ</h1>
    </div>
    <div id="form">
      <form @submit="getInfo" onsubmit="return false">
        <label for="cnpj">Digite um CNPJ</label>
        <input type="text" id="cnpj" minlength="14" maxlength="18" name="cnpj" placeholder="14707364000110"/>
        <button type="submit">Consultar</button>
      </form>
    </div>
    <nav class="grid">
      <emoji>🕵️</emoji>
      <div class="card" v-for="item in Object.keys(cnpjs)" v-bind:key="item">
        <div class="title">
          <p>{{ caseSensitive(item) }}</p>
        </div>
        <span></span>
        <div class="content">
          <p>{{ caseSensitive(cnpjs[item]) }}</p>
        </div>
      </div>
    </nav>
  </div> 
</template>

<script>
  import axios from 'axios';
  var mock = {"API OFFLINE 😥":"Este é um mock","NOME FANTASIA":"XCMG BRASIL INDUSTRIA","RAZAO SOCIAL":"XCMG BRASIL INDUSTRIA LTDA","CNPJ":"14707364000110","STATUS":"ATIVA","CNAE PRINCIPAL DESCRICAO":"Fabricação de máquinas e equipamentos para terraplenagem, pavimentação e construção, peças e acessórios, exceto tratores","CNAE PRINCIPAL CODIGO":"2854200","CEP":"37556830","DATA ABERTURA":"01/12/2011","DDD":"35","TELEFONE":"21020500","EMAIL":"fiscal@xcmg.com","TIPO LOGRADOURO":"RODOVIA","LOGRADOURO":"FERNAO DIAS - BR 381","NUMERO":"S/N","COMPLEMENTO":"KM 854/855","BAIRRO":"DISTRITO INDUSTRIAL (CDI)","MUNICIPIO":"Pouso Alegre","UF":"MG"}
  export default {
    name: 'Cnpjs',
    data() {
      return {
        cnpjs: [],
      };
    },
    methods: {
      getInfo: function() {
        let cnpj = document.getElementById('cnpj').value
        cnpj = filter(cnpj)
        axios
          .get(`https://www.receitaws.com.br/v1/cnpj/${cnpj}`)
          .then(res => {
              if (Array.isArray(res) && !res.length) {this.cnpjs = mock;}
              this.cnpjs = res.data;
          }).catch(error => {
              console.log(error);
              this.cnpjs = mock;
          })
      },
      filter: function(cnpjota) {
      	return cnpjota.split(".").join('').split('/').join('').split('-').join('')
      },
      caseSensitive: function(word) {
        let item = word.charAt(0).toUpperCase() + word.substring(1).toLowerCase()
        return item
      },
  },
}

</script>
<style>
  template {
    top: 60px;
  }
  * {
    font-family: 'Nunito', sans-serif;
  }
  :root {
    --clr-background: #eceff1;
    --clr-white: #D2CDEE;
    --clr-primary: #6847C2;
    --clr-gray: #263238;
    --clr-pink: #CB62B9;
    --clr-purple: #342D86;
    --clr-gray-black: #0E102A;
    --clr-black: #010402;
    --font-size: 16px;
    --border-radius: 0.2em;
  }
  #title {
    background-color: var(--clr-purple);
    background: #8e2de2;
    background: -webkit-linear-gradient(to right, #8e2de2, #4a00e0);
    background: linear-gradient(to right, #8e2de2, #4a00e0);
    max-width:300px;
    justify-content:center;
    transform: skew(-20deg, 0deg);
    margin: 0 auto;
    border: none;
    box-shadow: 5px 5px 0px 0px rgba(0, 0, 0, 1);
    -webkit-box-shadow: 5px 5px 0px 0px rgba(0, 0, 0, 1);
    transition: 200ms all;
  }
  #title:hover {
    background: -webkit-linear-gradient(to left, #8e2de2, #4a00e0);
    background: linear-gradient(to left, #8e2de2, #4a00e0);
    transform: scale(1.1) skew(-20deg, 0deg);
  }
  h1 {
    font-weight: bold;
    margin: 5%;
    color: var(--clr-primary);
    color: var(--clr-background);
  }
  label {
    color: var(--clr-white);
  }
  p {
    color: var(--clr-white);
  }
  body {
    background-color: var(--clr-background);
  }
  form {
    display: grid;
    gap:  10px;
  }
  .card {
    margin: 10px;
    border-radius: var(--border-radius);
    border: 0px solid var(--clr-pink);
    background: #6441a5;
    background: -webkit-linear-gradient(to right, #6441a5, #2a0845);
    background: linear-gradient(to right, #6441a5, #2a0845);
    transition: 200ms all;
  }
  .card:hover {
    transform: scale(1.1);
    background: #8e2de2;
    background: -webkit-linear-gradient(to right, #8e2de2, #4a00e0);
    background: linear-gradient(to right, #8e2de2, #4a00e0);
  }span {
    background: var(--clr-gray-black);
    height: 1px;
    width: 100%;
  }
  .card .title {
    padding-top: 5px;
    background-color: var(--clr-gray-black);
  }
  .card .content {
    padding-top: 5px;
  }
  button {
    height: 50px;
    font-weight: bold;
    color: var(--clr-white);
    border-radius: var(--border-radius);
    border: 2px solid var(--clr-white);
    border-right-width: 5% 5%;
    background: #8e2de2;
    background: -webkit-linear-gradient(to right, #8e2de2, #4a00e0);
    background: linear-gradient(to right, #8e2de2, #4a00e0);
    transition: 200ms all;
  }
  button:hover {
    background: #8e2de2;
    border: 1px solid var(--clr-purple);
  }
  input {
    height: 50px;
    padding-left: 20px;
    color: var(--clr-white);
    background-color: var(--clr-gray-black);
    font-weight: bold;
    border-radius: var(--border-radius);
    border: 1px solid var(--clr-primary);
  }
  nav {
    margin-top: 10px;
    border: 1px solid var(--clr-primary);
    border-radius: var(--border-radius);
    background-color: var(--clr-gray-black);
    color: var(--clr-white);
  }
  li {
    list-style: none;
  }
  [v-cloak] {
    display: none;
  }
</style>
