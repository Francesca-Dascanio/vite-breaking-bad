<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
    name: 'AppHeader',
}
</script>

<template>
    <div>
        <!-- Manca logo -->
        <div class="container">
            <h1>
                Yu-Gi-Oh API
            </h1>
        </div>
    </div>

</template>

<style lang="scss" scoped>
@use '../styles/partials/variables.scss' as *;

div {

    background-color: $secondary-color;

        .container {
            max-width: 1200px;
            margin: 0 auto;

            h1 {
                margin: 2rem 0;
            }
        }
}

</style>
