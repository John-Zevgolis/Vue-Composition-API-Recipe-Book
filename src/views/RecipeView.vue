<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">{{ recipe?.name }}</h1>
    <p class="mb-4">{{ recipe?.description }}</p>
    <div class="flex items-center gap-4">
      <RouterLink class="hover:underline" :to="{ name: 'edit-recipe', params: { id: recipe?.id } }"
        >Edit</RouterLink
      >
      <button
        class="px-4 py-2 bg-orange-600 text-white rounded hover:bg-orange-700"
        v-if="recipe"
        @click="recipeStore.toggleFavorite(recipe.id)"
      >
        {{ isFavorite ? 'Remove from favorites' : 'Add to favorites' }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useRecipeStore } from '@/stores/recipe';
import { computed } from 'vue';
import { useRoute, RouterLink } from 'vue-router';

const route = useRoute();

const recipeStore = useRecipeStore();

const recipe = computed(() => recipeStore.getRecipeById(route.params.id as string));

const isFavorite = computed(() => (recipe.value ? recipeStore.isFavorite(recipe.value.id) : false));
</script>
