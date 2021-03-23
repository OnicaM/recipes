<template>
    <div>
        <div class="button-addNew">
             <button @click.prevent="showAdd">Add new Recipe</button>
        </div>
        <div id="recipes">
            <ul class="recipes_list">
                <li :key="index" v-for="(recipe, index) in dataRecipes" @click="changeRecipe($event,index)">{{recipe.title}}</li>
            </ul>

            <div class="recipes_description">
                <div class="recipes_description-header">
                     <h3>{{dataRecipes[display].title}}</h3>
                     <div class="buttons-wrap">
                        <button @click.prevent="showUpdate" class="button button--edit">Edit</button>
                        <button @click="remove" class="button button--remove">Remove</button>
                     </div>
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
            this.$emit('indexChange', index);
        },
        showAdd: function(){
            this.$emit('show',true);
        },
        showUpdate: function(){
            this.$emit('updateShow',true);
        },
        remove: function(){
            this.$emit('remove', this.display);
        }
    }
}
export default recipes;
</script>
