<template id="consulta">
  <div class="container">
    <div id="title">
      <h1>ConsultaReceita</h1>
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
        cnpj = cnpj.split(".").join('').split('/').join('').split('-').join('')
        axios
          .get(`https://api-publica.speedio.com.br/buscarcnpj?cnpj=${cnpj}`)
          .then(res => {
              if (Array.isArray(res) && !res.length) {this.cnpjs = mock;}
              this.cnpjs = res.data;
          }).catch(error => {
              console.log(error);
              this.cnpjs = mock;
          })
      },
      caseSensitive: function(word) {
        let item = word.charAt(0).toUpperCase() + word.substring(1).toLowerCase()
        return item
      },
  },
}

</script>
<style>
  * {
    padding: 0;
    margin: 0;
    font-family: 'Nunito', sans-serif;
  }

  :root {
    --clr-background: #eceff1;
    --clr-background-two: #D2CDEE;
    --clr-primary: #5CA0D3;
    --clr-primary-variant: #7CA0D0;
    --clr-secondary: #C8E6F5;
    --clr-third: #6D3939;
    --clr-third-variant: #5E0A0A;
    --clr-foreground: #1f1f1f;
    --clr-black: #1E212D;
    --clr-white: #F2EEE0;
    --font-size: 16px;
    --border-radius: 0.5em;
  }
  
  button {
    height: 50px;
    font-weight: bold;
    color: var(--clr-white);
    border-radius: 0.5em;
    border: 1px solid var(--clr-foreground);
    transition: 200ms all;
    background: var(--clr-primary);
  }
  button:hover {
    background: var(--clr-primary-variant);
    border: 2px solid var(--clr-foreground);
    color: var(--clr-foreground);
  }
  #title {
    background: var(--clr-primary);
    max-width: 320px;
    justify-content: center;
    margin: 0 auto;
    border: none;
    border-radius: var(--border-radius);
    box-shadow: 2px 1px 0px 0px var(--clr-white);
    -webkit-box-shadow: 3px 3px 0px 0px var(--clr-black);
    transition: 200ms all;
  }
  #title:hover {
    transform: scale(1.1) skew(-20deg, 0deg);
  }
  h1 {
    font-weight: bold;
    margin: 5%;
    color: var(--clr-white);
  }

  label {
    color: var(--clr-foreground);
  }

  p {
    color: var(--clr-foreground);
  }

  form {
    display: grid;
    gap:  10px;
  }
  .card {
    margin: 10px;
    border-radius: var(--border-radius);
    border: 1px solid var(--clr-foreground);
    background: var(--clr-background);
    transition: 200ms all;
  }
  .card:hover {
    transform: scale(1.05);
    background: var(--clr-background);
  }
  span {
    background: var(--clr-background);
    color: var(--clr-foreground);
    height: 1px;
    width: 100%;
  }
  .card .title {
    border-top-left-radius: calc(var(--border-radius) - 0.1em);
    border-top-right-radius: calc(var(--border-radius) - 0.1em);
    background-color: var(--clr-primary-variant);
  }

  .card .title p {
    font-weight: bold;
    margin: auto;
    color: var(--clr-white);
  }
  .card .content {
    margin-top: 5px;
  }
  .card .content p {
    margin-top: 5px;
  }
  emoji:hover {
    transition: 300ms all;
    font-size: 25px;
  }
  input {
    height: 50px;
    padding-left: 20px;
    color: var(--clr-foreground);
    background-color: var(--clr-background);
    font-weight: bold;
    border-radius: var(--border-radius);
    border: 1px solid var(--clr-foreground);
    transition: 300ms all;
  }
  input:hover {
    background: var(--clr-foreground);
    border: 2px solid var(--clr-foreground);
    color: var(--clr-secondary);
  }
  nav {
    margin-top: 10px;
    background: var(--clr-background);
    border: none;
    border-radius: var(--border-radius);
    color: var(--clr-white);
  }
  li {
    list-style: none;
  }
  [v-cloak] {
    display: none;
  }
</style>
