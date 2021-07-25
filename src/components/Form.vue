<template>
  <div class="form">
    <form id="app" @submit="checkForm" method="post">
      <p v-if="errors.length">
        <b>Please correct the following error(s):</b>
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
      </p>
      <p>
        <label for="cnpj">Digite o CNPJ</label>
          <input type="number" name="cnpj" id="cnpj" v-model="cnpj"/>
      </p>
      <p>
        <input type="submit" value="Submit"/>  
      </p>
    </form>
  </div>
</template>

<script>

export default {
  name: 'Form',
  data() {
      return {
        cnpj: null,
        errors: [],
      };
    },
    checkForm: function(e) {
      if(this.cnpj.length >= 8) return true;
      if(!this.cnpj) this.errors.push("Precisa de um CNPJ.");
      e.preventDefault();
    }
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
