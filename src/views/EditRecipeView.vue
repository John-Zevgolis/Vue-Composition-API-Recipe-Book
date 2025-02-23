<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">Edit Form</h1>
  </div>
  <form class="space-y-4" @submit.prevent="updateRecipe">
    <div>
      <input
        class="p-2 border rounded w-full"
        type="text"
        v-model="name"
        placeholder="Recipe name"
        required
      />
    </div>
    <div>
      <textarea
        class="p-2 border rounded w-full"
        v-model="description"
        placeholder="Recipe description"
        required
      ></textarea>
    </div>
    <button class="px-4 py-2 bg-orange-600 text-white rounded hover:bg-orange-700" type="submit">
      Add
    </button>
  </form>
</template>

<script setup lang="ts">
import { useRecipeStore } from '@/stores/recipe';
import { ref, onMounted } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const name = ref('');
const description = ref('');

const router = useRouter();
const route = useRoute();

const store = useRecipeStore();

const fetchRecipe = () => {
  const id = route.params.id as string;
  const recipe = store.getRecipeById(id);
  if (recipe) {
    name.value = recipe.name;
    description.value = recipe.description;
  } else {
    router.push({ name: 'not-found' });
  }
};

onMounted(fetchRecipe);

const updateRecipe = () => {
  store.editRecipe({
    id: route.params.id as string,
    name: name.value,
    description: description.value,
  });

  router.push({
    name: 'recipe',
    params: {
      id: route.params.id as string,
    },
  });
};
</script>
