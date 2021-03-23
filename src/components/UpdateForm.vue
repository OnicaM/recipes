<template>
    <div>
        <div class="form-wrap">
            <form>
                <label for="addTitle">Recipe title</label>
                <input type="text" placeholder="Add title" id="addTitle" v-model="dataRecipes[recipeToDisplay].title" />
                <label>Ingrediens</label>
                <textarea cols="30" rows="10" v-model="dataRecipes[recipeToDisplay].ingredients"></textarea>
                <label>Directions</label>
                <textarea cols="30" rows="10" v-model="dataRecipes[recipeToDisplay].directions"></textarea>
                <input type="submit" class="button" value="Update" @click.prevent="update" />
            </form>
            <button @click="displayAll">click</button>
        </div>
        
    </div>
</template>

<script>
var updateForm = {
    props: {
        dataRecipes: {
            type: Array,
            required: true
        },
        recipeToDisplay:{
            type: Number,
            required: true
        },
        showUpdateForm: {
            type: Boolean,
            required: true
        }
    },
    data(){
        return{
            show: false,
            recipeTitle: '',
            recipeIngredients: '',
            recipeDirections:'',
            display: this.recipeToDisplay,
            joinIngredients: this.dataRecipes[recipeToDisplay].ingredients.join('/')
        }
    },
    methods: {
        displayAll: function(){
            console.log(this.dataRecipes[this.display]);
            this.joinIngredients = this.dataRecipes[this.display].ingredients.join('/');
            console.log(joinIngredients);
        },
        hideAdd: function(){
            this.$emit('hide',false);
            
        },
        update: function(){
           
            let ing = this.recipeIngredients.includes('/') ? this.recipeIngredients.split('/') : [this.recipeIngredients];
            let dir = this.recipeDirections.includes('/') ? this.recipeDirections.split('/') : [this.recipeDirections];
            this.$emit('updateR', {
                title: this.recipeTitle,
                ingredients: ing,
                directions: dir
            });
        }
    }
}

export default updateForm;
</script>
<style scoped>
label,
.button{
    display: block;
}
</style>