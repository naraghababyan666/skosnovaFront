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
              <h5 class="card-title">Получение категорий</h5>
              <p class="card-text">Get request returned all categories from database</p>
            </div>
          </div>
          <modal name="get-categories"
                 height="auto"
                 :scrollable="true"
                 :adaptive="true" >
            This is my first modal<br />
          </modal>
        </div>


        <div class="card text-white bg-success mb-3" style="width:100%">
          <div class="card-header">Header</div>
          <div class="card-body">
            <h5 class="card-title">Success card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
        <div class="card text-white bg-danger mb-3" style="width:100%">
          <div class="card-header">Header</div>
          <div class="card-body">
            <h5 class="card-title">Danger card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </main>

    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      getCategoriesAPIData: [],
    }
  },
  methods: {
    getCategoriesAPI(){
      console.log(this.getCategoriesAPIData)
      this.$modal.show('get-categories')
    }
  }
}
</script>

<style>

</style>
