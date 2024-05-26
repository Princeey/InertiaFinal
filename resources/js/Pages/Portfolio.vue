<script setup>
import { ref } from 'vue';
import { Head, Link, usePage } from '@inertiajs/vue3';
import { Inertia } from '@inertiajs/inertia';
import Mylayout from '@/Layouts/MyLayout.vue';
import EditModal from '@/Components/EditModal.vue';

defineOptions({
    layout: Mylayout,
});

const { props } = usePage();
const initialData = ref(props.aboutMeContent || 'Proceed to Characters');

const showModal = ref(false);

const openModal = () => {
    showModal.value = true;
};

const closeModal = () => {
    showModal.value = false;
};

const updateData = (data) => {
    initialData.value = data;
    // Update the backend to persist changes
    Inertia.put(route('about-me.update'), { content: data }, {
        onSuccess: () => {
            console.log('Data updated successfully');
        },
        onError: (errors) => {
            console.error('Error updating data:', errors);
        }
    });
};
</script>

<template>
    <Head title="About Me" />
    <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                <h1 class="text-4xl h1">About Genshin</h1>
                <hr />
                <p class="mt-[5%] text-center">{{ initialData }}</p>
                <div class="buttons marginb">
                    <button @click="openModal" class="but btn btn-pink hover:bg-yellow-400 transition duration-300 ease-in-out">Special Note</button>
                    <Link href="/project" class="but btn btn-pink hover:bg-yellow-400 transition duration-300 ease-in-out">Characters</Link>
                </div>
            </div>
        </div>
    </div>

    <EditModal :show="showModal" :initialData="initialData" @updatedData="updateData" @close="closeModal" />
</template>

<style scoped>
.marginb {
    margin-bottom: 50px;
}
.h1 {
    margin-top: 100px;
    margin-left: 100px;
    color: #2a65b7;
}
p {
    max-width: 800px;
    margin-left: 200px;
}
.buttons {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    margin-top: 40px;
}
.but {
    padding: 10px 20px;
    width: 200px;
    text-align: center;
    background-color: #133949; /* Summer theme color */
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
}
.but:hover {
    background-color: #ffb347; /* Lighter shade for hover effect */
}
</style>
