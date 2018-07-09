<template>
  <div id="app">
   
<b-navbar toggleable="md" type="dark" variant="info">

  <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

  <b-navbar-brand href="#"><h1 v-text="msg" :title="msg"></h1></b-navbar-brand>

  <b-collapse is-nav id="nav_collapse">

   
    <!-- Right aligned nav items -->
    <b-navbar-nav class="ml-auto">

      <b-form-input v-on:input="getdrinks(text1)" v-model="text1"
                  type="text"
                  placeholder="search"></b-form-input>
      
    </b-navbar-nav>
 

  </b-collapse>
</b-navbar>




   <template v-for="item in info.drinks">


<b-jumbotron>
  <template slot="header">
   {{item.strDrink}}
  </template>
  <template slot="lead">
    
   
      <b-img thumbnail fluid :src="item.strDrinkThumb" alt="Thumbnail" width="100px" />
  
  </template>
  <hr class="my-4">
  <p>

  </p>
  <b-btn variant="primary" v-b-modal="item.idDrink">View</b-btn>

 
</b-jumbotron>



    <b-col>
   

<!-- Modal Component -->
  <b-modal  :id="item.idDrink" :title="item.strDrink">
   <img class="" width="50%" :src="item.strDrinkThumb"></img>
    <p class="my-4">{{item.strCategory}}</p>
    <p class="my-4">{{item.strIBA}}</p>
    <p class="my-4">{{item.strAlcoholic}}</p>
     <p class="my-4">{{item.strGlass}}</p>
      <p class="my-4">{{item.strInstructions}}</p>
       <p class="my-4">{{item.strIngredient1}}</p>

  </b-modal>

    </b-col>

<template>
  <div>
    <b-button @click="showModal(item.idDrink)">
      Open Modal {{item.idDrink}}
    </b-button>
    <b-modal :ref="item.idDrink" hide-footer title="Using Component Methods">
      <div class="d-block text-center">
          <img class="" width="50%" :src="item.strDrinkThumb"></img>
    <p class="my-4">{{item.strCategory}}</p>
    <p class="my-4">{{item.strIBA}}</p>
    <p class="my-4">{{item.strAlcoholic}}</p>
     <p class="my-4">{{item.strGlass}}</p>
      <p class="my-4">{{item.strInstructions}}</p>
       <p class="my-4">{{item.strIngredient1}}</p>
      </div>
      <b-btn class="mt-3" variant="outline-danger" block @click="hideModal">Close Me</b-btn>
    </b-modal>
  </div>
</template>


     </template>




  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  data () {
    return {
      info: null,
      msg: 'Welcome to choise yours drinks',
      title: 'Aula de Vue',
      editMode: false,
      text1: '',
      frameworks: [
        {
          name: 'React',
          votes: 0
        }, {
          name: 'Angular',
          votes: 0
        }, {
          name: 'Vue',
          votes: 0
        }
      ]
    }
  },
  methods: {
     showModal (f) {  
      this.$refs.f.show()
    },
 hideModal (f) {
      this.$refs.f.hide()
    },
    toVote: function(f) {
      f.votes += 1
    }, 
    addFramework: function(event) {
      this.frameworks.push({
        name: event.target.value,
        votes: 0
      }),
      event.target.value = ''
    },
    removeFramework: function(f) {
      this.frameworks = this.frameworks.filter(i => i != f)
    },
    toggleEdit: function() {
      this.editMode = !this.editMode
    },
     getdrinks: function(f) {   
      axios.get('https://www.thecocktaildb.com/api/json/v1/1/search.php?s='+f)
  .then(response => (this.info = response.data))
    },
     getThisDrink: function(f) {   
  
    },
       
  },

mounted(){
  axios.get('https://www.thecocktaildb.com/api/json/v1/1/search.php?s=martini')
  .then(response => (this.info = response.data))
},


}



</script>




<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}

h1, h2 {
  font-weight: normal;
}

.jumbotron{
  width:50%;
      margin: 5px 25%;
}
</style>
