<template>
    <div>
        <div id="recipes">
            <ul class="recipes_list">
                <li :key="index" v-for="(recipe, index) in dataRecipes" @click="changeRecipe($event,index)">{{recipe.title}}</li>
            </ul>

            <div class="recipes_description">
                <div class="recipes_description-header">
                     <h3>{{dataRecipes[display].title}}</h3>
                     <button class="button button--remove">Remove</button>
                </div>
               
                <h4>Ingredients</h4>
                <ul>
                    <li :key="index" v-for="(ing, index) in dataRecipes[display].ingredients">{{ing}}</li>
                </ul>
                <h4>Directions</h4>
                <ol>
                    <li :key="index" v-for="(direction,index) in dataRecipes[display].directions">{{direction}}</li>
                </ol>
            </div>
        </div>
        

    </div>
</template>
<script>

var recipes = {
 
     props: {
        dataRecipes: {
            type: Array,
            required: true
        },
        recipeToDisplay:{
            type: Number,
            required: true
        },
        showAddForm: {
            type: Boolean,
            required: true
        }
    },
    data(){
        return{
            display: this.recipeToDisplay
        }
    },
    methods: {
        changeRecipe: function(event,index){
            this.display = index;
        }
    }
}
export default recipes;
</script>
