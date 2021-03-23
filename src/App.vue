<template>
  <div id="app">
    <app-header></app-header>
    
    <recipes 
    v-bind:dataRecipes="dataRecipes" 
    v-bind:recipeToDisplay="recipeToDisplay"
    v-bind:showAddForm="showAddForm">
    </recipes>
    <add-recipe-form v-bind:dataRecipes="dataRecipes" v-on:newR="addF($event)"></add-recipe-form>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Recipes from './components/Recipes.vue';
import AddForm from './components/AddForm.vue';
export default {
  name: 'app',
  components:{
    'app-header': Header,
    'recipes': Recipes,
    'add-recipe-form': AddForm
  },
  data () {
    return {
     dataRecipes: [],
     newRecipe: null,
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
    },
 
      methods: {
        addRecipe() {
          // ensure they actually typed something
          if (!this.newRecipe) {
            return;
          }

          this.dataRecipes.push(this.newRecipe);
          this.newRecipe = '';
          this.saveRecipes();
        },
        addF: function(newR){
          // this.dataRecipes = newR;
          
          this.dataRecipes = [...this.dataRecipes, newR];
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
