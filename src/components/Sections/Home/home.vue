<template>
    <section id="home" class="h-screen">
        <div>
            <Navbar />
        </div>
        <div>
            <header class="relative pt-16">
                <div class="container mx-auto">
                    <h1 class="text-6xl sm:text-7xl md:text-8xl font-extrabold tracking-tighter leading-none">
                        <span class="block text-white">Hello, I'm</span>
                        <span class="block text-emerald-400">Adexe Monzón Santana</span>
                    </h1>
                </div>
            </header>
        </div>
        
    </section>
</template>

<script>
import Navbar from '../../share/nav-component.vue';
    export default {
        name: 'Home',
        components: {
            Navbar,
        }
    }
</script>

<style lang="scss" scoped>

</style>