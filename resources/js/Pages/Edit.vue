<script setup>
  import { defineProps } from 'vue';
  import { useForm } from '@inertiajs/vue3';

  const props = defineProps({
    project: Object
  });

  const form = useForm({
    name: props.project.name,
    description: props.project.description,
    imageUrl: props.project.imageUrl,
  });

  const submitForm = async () => {
    await form.put(`/project/${props.project.id}`);
  };

  const goBack = () => {
    window.history.back();
  };

  let isHovered = false;
</script>

<template>
  <div class="container">
    <h1 class="display-4 title">Edit Project</h1>
    <div class="card form-container" :class="{ 'hovered': isHovered }" @mouseover="isHovered = true" @mouseleave="isHovered = false">
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name" class="label">Name:</label>
          <input v-model="form.name" type="text" class="form-control" id="name" placeholder="Enter project name">
        </div>
        <div class="form-group">
          <label for="description" class="label">Description:</label>
          <textarea v-model="form.description" class="form-control" id="description" placeholder="Enter project description" rows="5"></textarea>
        </div>
        <div class="form-group">
          <label for="imageUrl" class="label">Image URL:</label>
          <input v-model="form.imageUrl" type="text" class="form-control" id="imageUrl" placeholder="Enter image URL">
        </div>
        <div class="btn-group">
          <button @click="goBack" type="button" class="btn btn-secondary">Back</button>
          <button type="submit" class="btn btn-primary">Save</button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
  .container {
    max-width: 600px;
    margin: 40px auto;
    padding: 20px;
    background-color: #ADD8E6; /* Summer theme background color */
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  .title {
    margin-bottom: 20px;
    color: #7952b3; /* Bootstrap purple */
  }

  .form-container {
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    transition: box-shadow 0.3s ease, transform 0.3s ease;
  }

  .form-container.hovered {
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    transform: translateY(-5px);
  }

  .label {
    display: block;
    margin-bottom: 10px;
    color: #495057; /* Bootstrap gray */
  }

  .form-group {
    margin-bottom: 20px;
  }

  .form-control {
    width: 100%;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid #ced4da; /* Bootstrap gray */
    transition: border-color 0.3s ease;
    outline: none;
  }

  .form-control:hover,
  .form-control:focus {
    border-color: #6c757d; /* Bootstrap gray on hover/focus */
  }

  .btn-group {
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  .btn {
    padding: 10px 20px;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    outline: none;
  }

  .btn-primary {
    background-color: #007bff; /* Bootstrap blue */
    color: #fff;
    border: none;
  }

  .btn-secondary {
    background-color: #6c757d; /* Bootstrap gray */
    color: #fff;
    border: none;
    margin-right: 10px;
  }

  .btn-primary:hover,
  .btn-secondary:hover {
    filter: brightness(0.9);
    transform: translateY(-2px); /* Move button slightly up on hover */
  }
</style>