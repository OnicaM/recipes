<template>
    <div>
        <div class="form-wrap form-wrap--add">
            <button @click.prevent="closeForm" class="close">X</button>
            <h3>Add new recipe</h3>
            <form>
                <label for="addTitle">Recipe title</label>
                <input type="text" placeholder="Add title" id="addTitle" v-model="recipeTitle"/>
                <label>Ingrediens</label>
                <textarea id="" cols="30" rows="5" v-model="recipeIngredients" placeholder="Separate each ingredient with a '\': Milk \ 2 Eggs \ 1/3 Cup Sugar"></textarea>
                <label>Directions</label>
                <textarea id="" cols="30" rows="5" v-model="recipeDirections" placeholder="Separate each ingredient with a '\': Milk \ 2 Eggs \ 1/3 Cup Sugar"></textarea>
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
        },
        showAddForm:{
            type:Boolean
        }
    },
    data(){
        return{
            show: false,
            recipeTitle: '',
            recipeIngredients: '',
            recipeDirections:'',
        }
    },
    methods: {
        closeForm: function(){
            this.$emit('closeForm', false);
        },
       
        add: function(){
            let ing = this.recipeIngredients.includes('/') ? this.recipeIngredients.split('/') : [this.recipeIngredients];
            let dir = this.recipeDirections.includes('/') ? this.recipeDirections.split('/') : [this.recipeDirections];
            this.$emit('newR', {
                title: this.recipeTitle,
                ingredients: ing,
                directions: dir
            });
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