<template>
    <div>
        <div class="form-wrap form-wrap--update">
            <button @click="closeForm" class="close">X</button>
            <h3>Edit your recipe</h3>
            <form>
                <label for="addTitle">Recipe title</label>
                <input type="text" placeholder="Add title" id="addTitle" ref="title" />
                <label>Ingrediens</label>
                <textarea cols="30" rows="5" ref="ingredients" placeholder="Separate each ingredient with a '\': Milk \ 2 Eggs \ 1/3 Cup Sugar"></textarea>
                <label>Directions</label>
                <textarea cols="30" rows="5" ref="directions" placeholder="Separate each ingredient with a '\': Milk \ 2 Eggs \ 1/3 Cup Sugar"></textarea>
                <button class="button"  @click.prevent="update"> Update </button>
            </form>
            
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
            joinIngredients:''
        }
    },
    methods: {
        closeForm: function(){
            this.$emit('closeForm', false);
        },
        hideAdd: function(){
            this.$emit('hide',false);
            
        },
        update: function(){
            
            var notEmptyIng = this.$refs.ingredients.value != ''? this.$refs.ingredients.value : this.dataRecipes[this.recipeToDisplay].ingredients.join('/');
            var notEmptyDir = this.$refs.directions.value != ''? this.$refs.directions.value : this.dataRecipes[this.recipeToDisplay].ingredients.join('/');
            let ing = notEmptyIng.includes('/') ? this.$refs.ingredients.value.split('/') : [this.$refs.ingredients.value];
            let dir = notEmptyDir.includes('/') ? this.$refs.directions.value.split('/') : [this.$refs.directions.value];
            
            if(this.$refs.title.value !='' && this.$refs.directions.value !='' && this.$refs.ingredients.value !=''){
                this.$emit('updateR', {
                    recipeId: this.recipeToDisplay,
                    title: this.$refs.title.value,
                    ingredients: ing,
                    directions: dir
                });
            }else{
                alert('Please fill all fileds');
            }
           
            
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