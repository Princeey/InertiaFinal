<script setup>
import MyLayout from '@/Layouts/MyLayout.vue';
import { useForm } from '@inertiajs/vue3';
import { Link } from "@inertiajs/vue3";

defineOptions({
  layout: MyLayout
});

const { project } = defineProps(['project']);

const projectForm = useForm({
  initialValues: {
    name: project.name,
    description: project.description,
    imageUrl: project.category_id,
  }
});

// Function to handle project deletion
const deleteProject = async (projectToDelete) => {
  try {
    const confirmed = confirm("Are you sure you want to delete?");
    if (confirmed) {
      await projectForm.delete(`/project/${projectToDelete.id}`, { preserveScroll: true });
      // Handle success or other actions after deletion
    }
  } catch (error) {
    console.error('Error deleting project:', error.message);
    // Handle error appropriately, e.g., show an error message to the user
  }
};
</script>

<template>
  <div class="mt-8">
    <div class="flex justify-between items-center mt-10 ml-2">
      <div class="flex items-center space-x-4">
        <Link href='/portfolio' class="btn arrow text-green-500">←</Link>
        <h1 class="text-4xl font-bold text-green-500">Characters</h1>
      </div>
      <div class="mr-1">
        <Link href='/project/create' class="btn bg-yellow-400 text-white font-bold py-2 px-4 rounded">Add Favorite Character</Link>
      </div>
    </div>

    <div class="overflow-auto h-60vh p-2 container">
      <transition-group name="fade" tag="div" appear>
        <div v-for="projectItem in project" :key="projectItem.id" class="mt-2 border p-2 bg-yellow-100 rounded" style="animation-delay: 0.3s">
          <div class="flex gap-2">
            <div class="w-1/2">
              <img :src="projectItem.imageUrl" :alt="'Image for ' + projectItem.name" class="w-full rounded h-40 object-cover" style="animation-delay: 0.3s">
            </div>
            <div class="w-full flex flex-col justify-between">
              <div>
                <div class="flex items-center">
                  <h1 class="text-4xl flex-1 font-bold text-green-500">{{ projectItem.name }}</h1>
                  <button @click="deleteProject(projectItem)" class="btn btn-delete">X</button>
                </div>
                <p class="text-center">{{ projectItem.description }}</p>
              </div>
              <div class="flex justify-end">
                <Link :href="`/project/${projectItem.id}/edit`" class="btn bg-yellow-300 text-white p-2">
                  <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="currentColor" class="bi bi-sun" viewBox="0 0 16 16">
                    <path fill-rule="evenodd" d="M11.5 8a3.5 3.5 0 1 1-7 0 3.5 3.5 0 0 1 7 0zm1.5 0a5 5 0 1 0-10 0 5 5 0 0 0 10 0zm-6 3a1 1 0 0 0 .707 1.707 1 1 0 0 0 1.414-1.414A1 1 0 0 0 7 11zm1.5-5a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm0 5a.5.5 0 0 1-.5-.5V8a.5.5 0 0 1 1 0v1a.5.5 0 0 1-.5.5zm3.5-4a.5.5 0 0 0 .5-.5A.5.5 0 0 0 13 6a.5.5 0 0 0-.5.5.5.5 0 0 0 .5.5zm-9 0a.5.5 0 0 0-.5-.5.5.5 0 0 0-.5.5.5.5 0 0 0 .5.5zm9 0a.5.5 0 0 0-.5-.5.5.5 0 0 0-.5.5.5.5 0 0 0 .5.5zm-9 0a.5.5 0 0 0-.5-.5.5.5 0 0 0-.5.5.5.5 0 0 0 .5.5z"/>
                  </svg>
                </Link>
              </div>
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<style scoped>
/* General styles */
.text-4xl {
  font-size: 2.25rem;
}

.font-bold {
  font-weight: bold;
}

.text-center {
  text-align: center;
}

.btn {
  display: inline-block;
  text-decoration: none;
  cursor: pointer;
}

.rounded {
  border-radius: 0.25rem;
}

/* Arrow button styles */
.arrow {
  color: #00cc66; /* Summer green */
  font-size: 2.25rem;
}

.arrow:hover {
  color: #00ff99; /* Lighter green on hover */
}

/* Delete button styles */
.btn-delete {
  background-color: #ff6666; /* Coral red */
  color: #fff;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem; 
}

.btn-delete:hover {
  background-color: #ff3333; /* Darker red on hover */
}

/* Fade animation */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s, transform 0.5s ease-in-out;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
  transform: translateY(20px); /* Change translateY to move items upside down */
}
</style>


