<template>
  <div class="home">
    <h1>Lista de Empresas</h1>
    <div>
      <table class="tb">
        <tr>
          <th>Nombre</th>
          <th>Categoria</th>
          <th>Descripcion</th>
        </tr>
        <tr v-for="c in companies" :key="c._id">
          <td>{{c.company_name}}</td>
          <td>{{c.category}}</td>
          <td>{{c.description}}</td>
        </tr>
      </table>
    </div>
    <h1>Registar nueva empresa</h1>
    <div>
      <div class="form-item">
        <label class="form-label">Nombre de la empresa</label>
        <input type="text" v-model="new_company.company_name"/>
      </div>
      <div class="form-item">
        <label class="form-label">Descripcion de la empresa</label>
        <input type="text" v-model="new_company.description"/>
      </div>
      <div class="form-item">
        <label class="form-label">Categoria</label>
        <input type="text" v-model="new_company.category"/>
      </div>
      <div class="form-item">
        <label class="form-label">URL logo de la empresa</label>
        <input type="text" v-model="new_company.logo"/>
      </div>
      <div class="form-item">
        <input type="button" value="Registrar producto" v-on:click="postCompany"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    
  },
  data(){
    return{
      companies: null,
      new_company: {
        company_name: '',
        description: '',
        category: '',
        logo: ''
      }
    }
  },
  created(){
    this.getCompanies();
  },
  methods: {
    getCompanies(){
      axios.get('http://localhost:3000/api/companies')
      .then(response =>{
        this.companies = response.data;
      })
      .catch(error =>{
        console.log(error);
      })
    },
    postCompany(){
      axios.post('http://localhost:3000/api/companies/new', this.new_company)
      .then(response =>{
        console.log(response.data);
        this.getCompanies();
      })
      .catch(error =>{
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>
.tb {
  border: 1px solid;

}

td {
  border: 1px solid;
  padding: 5px;
}

.form-item {
  padding: 10px;
}

.form-label{
  padding: 20px; 
}
</style>
