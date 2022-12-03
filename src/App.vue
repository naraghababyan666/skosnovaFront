<template>
  <div id="app">
    <div class="container d-flex h-100 p-3 mx-auto flex-column">
      <header class="masthead ">
        <div class="inner">
          <h3 class="masthead-brand">Cover</h3>
          <nav class="nav nav-masthead justify-content-center">
            <a class="nav-link active" href="#">Home</a>
            <a class="nav-link" href="#">Features</a>
            <a class="nav-link" href="#">Contact</a>
          </nav>
        </div>
      </header>

      <main role="main" class="inner cover">
        <div class="get-categories">
          <div class="card text-white bg-primary mb-3" style="width:100%" @click="getCategoriesAPI">
            <div class="card-header">GET - /categories</div>
            <div class="card-body">
              <h5 class="card-title">Get all categories</h5>
              <p class="card-text">Get request returned all categories from database</p>
            </div>
          </div>
          <modal name="get-categories"
                 height="auto"
                 width="80%"
                 :scrollable="true"
                 :adaptive="true" >
            <table class="table table-hover categories-parent">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Name</th>
                  <th scope="col">Parent id</th>
                  <th scope="col">Created at</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="item in this.getCategoriesAPIData" :key="item.id" class="category">
                  <th scope="row">{{item.id}}</th>
                  <td>{{ item.name }}</td>
                  <td>{{ item.parent_id }}</td>
                  <td>{{ item.created_at }}</td>
                </tr>
              </tbody>
            </table>
          </modal>
        </div>
        <div class="create-category">
          <div class="card text-white bg-success mb-3" style="width:100%">
            <div class="card-header">POST - /categories</div>
            <div class="card-body">
              <h5 class="card-title">Create category, insert name and parent category if exists</h5>
              <p class="card-text">Insert category name - <input type="text" v-model="categoryNameForCreateCategory" style="margin-left: 10px;" /> </p>
              <p class="card-text d-flex" >Choose parent category -
                <select class="form-select form-select-sm" style="width: auto; margin-left: 15px;">
                  <option selected value="null">Categories</option>
                  <option v-for="item in getCategoriesAPIDataGlobal" :key="item.id" @click="chooseParentCategoryForCreateCategory = item.id">{{item.name}}</option>
                </select>
              </p>
              <button type="button" @click="createCategory"  class="btn btn-dark">Test API</button>
            </div>
            <modal name="create-categories"
                   height="auto"
                   width="80%"
                   :scrollable="true"
                   :adaptive="true" >
              <p class="success-message">Category successfully created</p>
            </modal>
          </div>
        </div>
        <div class="update-category">
          <div class="card text-white bg-secondary ">
            <div class="card-header">POST - /categories/{ID}</div>
            <div class="card-body">
              <h5 class="card-title">Secondary card title</h5>
              <div v-for="item in getCategoriesAPIDataGlobal" :key="item.id">
                <div  class="d-flex justify-content-between content">
                  <span>{{item.id}} | {{item.name}}</span>  <button  @click="getCategoryByIdAPI(item.id)" type="button" class="btn btn-dark">Edit</button>
                </div>
              </div>
              <div>
                <div >
                  <h1>asdasd</h1>
                </div>
              </div>
            </div>
            <modal name="getCategoryById-modal"
            height="auto"
            width="80%"
            :scrollable="true"
            :adaptive="true"
            v-if="getCategoryDataForUpdate != null">

              <input type="text" :value="this.getCategoryDataForUpdate.name"/>
            </modal>
          </div>
        </div>

        <hr />


        <div class="get-products">
          <div class="card text-white bg-primary mb-3" style="width:100%" @click="getProductsAPI">
            <div class="card-header">GET - /products</div>
            <div class="card-body">
              <h5 class="card-title">Get products list</h5>
              <p class="card-text">Get request returned all products from database</p>
            </div>
          </div>
          <modal name="get-products"
                 width="80%"
                 height="auto"
                 :scrollable="true"
                 :adaptive="true" >
            <table class="table table-hover products-parent">
              <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Name</th>
                <th scope="col">Parent id</th>
                <th scope="col">Created at</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="item in this.getProductsAPIData" :key="item.id" class="category">
                <th scope="row">{{item.id}}</th>
                <td>{{ item.name }}</td>
                <td>{{ item.price }}</td>
                <td>{{ item.category_id }}</td>
                <td>{{ item.created_at }}</td>
              </tr>
              </tbody>
            </table>
          </modal>

        </div>
        <div class="create-products">
          <div class="card text-white bg-success mb-3" style="width:100%">
            <div class="card-header">POST - /products</div>
            <div class="card-body">
              <h5 class="card-title">Create product, insert name,price and category</h5>
              <p class="card-text">Insert product name - <input type="text" v-model="productNameForCreate" style="margin-left: 10px;"/> </p>
              <p class="card-text">Insert product price - <input type="number" v-model="productPriceForCreate" style="margin-left: 10px;" /> </p>
              <p class="card-text d-flex" >Choose category -
                <select class="form-select form-select-sm" style="width: auto; margin-left: 15px;">
                  <option selected value="null">Categories</option>
                  <option v-for="item in getCategoriesAPIDataGlobal" :key="item.id" @click="this.chooseCategoryForCreateProduct = item.id">{{item.name}}</option>
                </select>
              </p>
              <button type="button" @click="createProduct"  class="btn btn-dark">Test API</button>
            </div>
            <modal name="create-products"
                   height="auto"
                   width="80%"
                   :scrollable="true"
                   :adaptive="true" >
              <p class="success-message">Product successfully created</p>
            </modal>
          </div>
        </div>
        <div class="delete-products">

          <div class="card text-white bg-danger mb-3" style="width:100%">
            <div class="card-header">DELETE - /products/{ID}</div>
            <div class="card-body">
              <h5 class="card-title">Delete product, insert ID.</h5>
              <p class="card-text">Insert product price - <input type="number" v-model="productIdForDelete" style="margin-left: 10px;" /> </p>

              <button type="button" @click="deleteProductById(productIdForDelete)"  class="btn btn-dark">Test API</button>
            </div>
            <modal name="delete-products"
                   height="auto"
                   width="80%"
                   :scrollable="true"
                   :adaptive="true" >
              <p class="success-message">Product successfully deleted</p>
            </modal>
          </div>
        </div>


        <modal name="success-modal"
               height="auto"
               width="80%"
               :scrollable="true"
               :adaptive="true" >
          <p class="success-message">Product successfully created</p>
        </modal>
      </main>

    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data(){
    return {
      getCategoriesAPIData: [],
      getProductsAPIData: [],
      getCategoriesAPIDataGlobal: [],
      chooseParentCategoryForCreateCategory: null,
      chooseCategoryForCreateProduct: null,
      categoryNameForCreateCategory: null,
      productPriceForCreate: 0,
      productNameForCreate: null,
      productIdForDelete: null,
      getCategoryDataForUpdate: null,
    }
  },
  components: {
    // eslint-disable-next-line vue/no-unused-components
    axios
  },
  mounted() {
    this.getCategoriesAPIGlobal();
    // axios.get("http://127.0.0.1:8000/api/makePassword/6").then((res) => {
    //   console.log(res.data)
    // })
  },
  methods: {
    getCategoriesAPI(){
      axios.get("http://127.0.0.1:8000/api/categories").then((res) => {
        if(res.data.success){
          this.getCategoriesAPIData = res.data.categories
          this.$modal.show('get-categories')
        }
      })
    },
    getCategoriesAPIGlobal(){
      axios.get("http://127.0.0.1:8000/api/categories").then((res) => {
        if(res.data.success){
          this.getCategoriesAPIDataGlobal = res.data.categories
        }
      })
    },
    getCategoryByIdAPI(id){
      console.log(id)
      axios.get("http://127.0.0.1:8000/api/categories/" + id).then((res) => {
        if(res.data.success){
          this.getCategoryDataForUpdate = res.data.data;
          this.$modal.show('getCategoryById-modal', this.getCategoryDataForUpdate)

        }
        // this.$modal.show('getCategoryById-modal', {'category_id' : item.id})
        // if(res.data.success){
        //   this.getCategoriesAPIData = res.data.categories
        //   this.$modal.show('get-categories')
        // }
      })
    },
    getProductsAPI(){
      axios.get("http://127.0.0.1:8000/api/products").then((res) => {
        if(res.data.success){
          this.getProductsAPIData = res.data.products
          this.$modal.show('get-products')
        }
      })
    },

    createCategory(){
      if(this.categoryNameForCreateCategory != null){
        axios.post("http://127.0.0.1:8000/api/categories", {
          'name' : this.categoryNameForCreateCategory,
          'parent_id' : this.chooseParentCategoryForCreateCategory
        }).then((res) => {
          if(res.data.success){
            this.$modal.show('create-categories')
          }
        })
      }else{
        alert('Insert category name')
      }
    },
    createProduct(){
      if(this.productNameForCreate != null && this.chooseCategoryForCreateProduct != null && this.productPriceForCreate !== 0){
        axios.post("http://127.0.0.1:8000/api/products", {
          'name' : this.productNameForCreate,
          'price' : this.productPriceForCreate,
          'category_id' : this.chooseCategoryForCreateProduct
        }).then((res) => {
          if(res.data.success){
            this.$modal.show('create-products')
          }
        })
      }else{
        console.log(this.chooseCategoryForCreateProduct, this.productPriceForCreate, this.productNameForCreate)
      }
    },
    deleteProductById(id){
      // axios.delete("")
      if(id != null || id !== 0){
        axios.delete("http://127.0.0.1:8000/api/products/"+id).then((res) => {
          if(res.data.success){
            this.$modal.show('delete-products')
          }
        })
      }
    }
  }
}
</script>

<style>
.categories-parent{
  width: auto;
  margin: 20px;
  color: black;
}
.vm--modal{
  display: flex;
  align-content: center;
  justify-content: center;
}
input[type="text"]{
  background-color: white !important;
  border-radius: 0.25rem;
  border:none;
  outline: none;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type=number] {
  -moz-appearance: textfield;
  border-radius: 0.25rem;
  border: none;
  outline: none;
}
.success-message{
  padding: 40px;
  color: green;
}
.form-select{
  border:none;
  outline: none;
}
</style>
