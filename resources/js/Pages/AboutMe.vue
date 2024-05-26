<script setup>
import MyLayout from '@/Layouts/MyLayout.vue';
import { Link } from '@inertiajs/vue3';

defineOptions({
    layout: MyLayout
})
</script>

<template>

    <div class="container">
        <div class="aboutme">
            <h1>About Me</h1>
            <hr>
            <p>I'm Prince Paul Banquil, a web developer with a passion for crafting immersive online experiences. From sleek websites to seamless functionality, I thrive on turning ideas into reality. Let's build something awesome together!</p>
        </div>
        <br>
        <br>
        <br>
        <br>
        <main>
        <div class="btns">
            <button>Resume</button>
            <Link class="port" href="/port">Portfolio</Link>
        </div>
    </main>
    </div>
    <footer>
        <div class="socials">
            <a href="#" id="icon" class="social-icon"><i class="fa-brands fa-instagram"></i></a>
            <a href="#" id="icon" class="social-icon"><i class="fa-brands fa-twitter"></i></a>
            <a href="#" id="icon" class="social-icon"><i class="fa-brands fa-facebook"></i></a>
            <a href="#" id="icon" class="social-icon"><i class="fa-brands fa-linkedin"></i></a>
        </div>
    </footer>

</template>

<style scoped>
.container {
    position: relative;
    width: 100%;
    padding: 60px;
}

.aboutme {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

button {
    border: 1px solid black;
    padding: 10px;
    width: 15%;
    font-weight: bold;
}

hr {
    border: 1px solid black;
}

.btns {
    display: flex;
    gap: 30px;
}

.port {
    border: 1px solid black;
    padding: 10px;
    width: 15%;
    text-align: center;
    font-weight: bold;
}

h1 {
    font-size: 30px;
}

.socials {
    position: absolute;
    bottom: 20px;
    right: 20px;
    display: flex;
    gap: 20px;
}

.social-icon {
    font-size: 20px;
    background-color: black;
    color: white;
    border-radius: 10px;
    padding: 5px 10px 5px 10px;
}
</style>
