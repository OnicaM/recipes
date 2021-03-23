<template>
    <div>
        <button @click="showMore" >Add new Recipe</button>
        <div class="form-wrap" v-show="show">
            <form>
                <label for="addTitle">Recipe title</label>
                <input type="text" placeholder="Add title" id="addTitle" v-model="recipeTitle"/>
                <label>Ingrediens</label>
                <textarea id="" cols="30" rows="10" v-model="recipeIngredients"></textarea>
                <label>Directions</label>
                <textarea id="" cols="30" rows="10" v-model="recipeDirections"></textarea>
                <input type="submit" class="button" value="Add" @click.prevent="add" />
            </form>
        </div>
        <p>Title: {{recipeTitle}}</p>
        <p>Ingredients: {{recipeIngredients}}</p>
        <p>Directions: {{recipeDirections}}</p>
    </div>
</template>

<script>
var addForm = {
    props:{
         dataRecipes: {
            type: Array,
            required: true
        }
    },
    data(){
        return{
            show: false,
            recipeTitle: '',
            recipeIngredients: '',
            recipeDirections:''
        }
    },
    methods: {
        showMore: function(){
            this.show= !this.show;
        },
        add: function(){
            this.$emit('newR', {
                title: this.recipeTitle,
                ingredients: this.recipeIngredients,
                directions: this.recipeDirections
            });
           console.log(this.recipeTitle + "\n" + this.recipeIngredients + "\n" + this.recipeDirections);
        }
    }
}

export default addForm;
</script>
<style scoped>
label,
.button{
    display: block;
}
</style>