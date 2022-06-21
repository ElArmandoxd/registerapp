<template>
  <div class="about">
    <h1>Lista de productos</h1>
    <div>
      <table class="tb">
        <tr>
          <th>Nombre</th>
          <th>Vendedor</th>
          <th>Descripcion</th>
          <th>Precio</th>
          <th>ID stripe</th>
        </tr>
        <tr v-for="p in products" :key="p._id">
          <td>{{p.name}}</td>
          <td>{{p.company_name}}</td>
          <td>{{p.description}}</td>
          <td>$ {{p.price}}.00 MXN</td>
          <td>{{p.stripe_price}}</td>
        </tr>
      </table>
    </div>
    <h1>Registar nuevo producto</h1>
    <div>
      <div class="form-item">
        <label class="form-label">Nombre del producto</label>
        <input type="text" v-model="new_product.name"/>
      </div>
      <div class="form-item">
        <label class="form-label">Descripcion del producto</label>
        <input type="text" v-model="new_product.description"/>
      </div>
      <div class="form-item">
        <label class="form-label">Nombre del vendedor</label>
        <input type="text" v-model="new_product.company_name"/>
      </div>
      <div class="form-item">
        <label class="form-label">ID del vendedor</label>
        <input type="text" v-model="new_product.company_id"/>
      </div>
      <div class="form-item">
        <label class="form-label">URL imagen del producto</label>
        <input type="text" v-model="new_product.image"/>
      </div>
      <div class="form-item">
        <label class="form-label">Precio en numero</label>
        <input type="number" v-model="new_product.price"/>
      </div>
      <div class="form-item">
        <label class="form-label">Precio ID stripe</label>
        <input type="text" v-model="new_product.stripe_price"/>
      </div>
      <div class="form-item">
        <input type="button" value="Registrar producto" v-on:click="postProduct"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return{
      products: null,
      new_product: {
        name: '',
        company_id: '',
        description: '',
        image: '',
        company_name: '',
        price: 0,
        stripe_price: ''
      }
    }
  },
  created(){
    this.getProducts()
  },
  methods:{
    getProducts() {
      axios.get('http://localhost:3000/api/products')
      .then(response =>{
        this.products = response.data;
      })
      .catch(error =>{
        console.log(error);
      })
    },
    postProduct(){
      axios.post('http://localhost:3000/api/products/new', this.new_product)
      .then(response =>{
        console.log(response.data);
        this.getProducts();
      })
      .catch(error =>{
        console.log(error);
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
