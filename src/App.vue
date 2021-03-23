<template>
  <div id="app">
    <app-header></app-header>
    
    <recipes 
      v-bind:dataRecipes="dataRecipes" 
      v-bind:recipeToDisplay="recipeToDisplay"
      v-bind:showAddForm="showAddForm"
      v-on:show="showaddForm($event)"
      v-on:remove="removeRecipe($event)">
    </recipes>
    <add-recipe-form 
    v-bind:dataRecipes="dataRecipes" 
    v-on:newR="addF($event)"
    v-show="showAddForm" v-on:hideAdd="hideAddForm($event)"></add-recipe-form>

    <update-form 
    v-bind:dataRecipes="dataRecipes" 
    v-bind:recipeToDisplay="recipeToDisplay"
    v-on:updateR="updateF($event)"
    v-bind:showUpdateForm="showUpdateForm"
    v-on:show="showUpdate($event)"></update-form>
  </div>


</template>

<script>
import Header from './components/Header.vue';
import Recipes from './components/Recipes.vue';
import AddForm from './components/AddForm.vue';
import UpdateForm from './components/UpdateForm.vue';

export default {
  name: 'app',
  components:{
    'app-header': Header,
    'recipes': Recipes,
    'add-recipe-form': AddForm,
    'update-form': UpdateForm
  },
  data () {
    return {
     dataRecipes: [],
     show: false,
     url: '',
     recipeToDisplay: 1,
     showAddForm: false,
     showUpdateForm: false
    }
  },
   mounted(){
      this.$http.get('http://localhost:8080/src/db/db.json').then(function(data){
      //  this.dataRecipes = data.body;
        let parsed = JSON.stringify(data.body);
        localStorage.setItem('recipes', parsed);
      });
      if (localStorage.getItem('recipes')) {
        try {
          this.dataRecipes = JSON.parse(localStorage.getItem('recipes'));
        } catch(e) {
          localStorage.removeItem('recipes');
        }
      }
      console.log("array ",this.dataRecipes);
    },
 
    methods: {
      hideAddForm: function(hide){
        this.showAddForm = hide;
        console.log(hide);
      },
      showaddForm: function(show){
        this.showAddForm = !this.showAddForm;
        console.log(show);
      },
      showUpdate: function(update){
        this.showUpdateForm = update;
        console.log(update);
      },
      addF: function(newR){
        // this.dataRecipes = newR;
        
        this.dataRecipes.push(newR);
        this.saveRecipes();
      },
      updateF: function(update){
        // this.dataRecipes = newR;
        
        this.dataRecipes.push(update);
        this.saveRecipes();
      },
      removeRecipe(x) {
        this.dataRecipes.splice(x, 1);
        this.saveRecipes();
      },
      saveRecipes() {
        const parsed = JSON.stringify(this.dataRecipes);
        localStorage.setItem('recipes', parsed);
      }
      
    }
   
}
</script>

<style>

</style>
