<template>
  <RecipeItem 
  :image="recipe.recipe.image" 
  :label="recipe.recipe.label" 
  :attributes="recipe.recipe.dietLabels.join(', ')" 
  :url="recipe.recipe.url"
  v-for="recipe in recipes" />
</template>

<script>
import RecipeItem from '@/components/RecipeItem.vue';
export default {
  components: {
    RecipeItem
  },
  data() {
    return {
      recipes: []
    }
  },
  methods: {
    async getRecipes() {
      const query = 'sushi';
      const appId = 'e079e210';
      const appKey = '496d2aa4bf48ba186176e315e9b185bb';
      const url = `https://api.edamam.com/search?q=${query}&app_id=${appId}&app_key=${appKey}`;
      let resp = await fetch(url);
      this.recipes = (await resp.json()).hits;
    }
  },
  mounted() {
    this.getRecipes();
  }
}
</script>
