<template>
  <div>
    <nav v-if="recipes.length > 0">
      <ul>
        <li class="mb-2" v-for="recipe in recipes" :key="recipe.id">
          <RouterLink
            class="text-amber-600 hover:underline"
            :to="{ name: 'recipe', params: { id: recipe.id } }"
            >{{ recipe.name }}</RouterLink
          >
        </li>
      </ul>
    </nav>
    <div class="text-gray-500" v-else>No recipes found!</div>
  </div>
</template>

<script setup lang="ts">
import type { Recipe } from '@/stores/recipe';
import { RouterLink } from 'vue-router';

defineProps<{
  recipes: Recipe[];
}>();
</script>
