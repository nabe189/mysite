<template>
    <v-app class="grey lighten-4">
        <Navbar />
        <v-content>
            <v-container fluid fill-height>
                    <router-view></router-view>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import Navbar from '@/components/Navbar'
export default {
    name: 'App',
    components: {
        Navbar
    }
}
</script>

<style>
.wrapper {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    background-color: black;
    width: 100%;
}
@media (min-width: 576px) {
    .wrapper {
        overflow: hidden;
    }
} 