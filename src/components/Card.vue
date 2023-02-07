<script>
import { store } from '../store';

export default {
    name: 'Card',
    data () {
        return {
            store
        }
    },
    props: {
        card: Object
    },
    methods: {
        filterCards: function () {
            
        }
    }
}
</script>

<template>
    
    <div class="card-image">
        <img :src="card.card_images[0].image_url" :alt="card.name">
    </div>
    <div class="card-text">
        <div>
            {{ card.name }}
        </div>
        <div>
            {{ card.archetype }}
        </div>
    </div>

</template>

<style lang="scss" scoped>

.card-image {
    max-width: 100%;
    height: auto;

    img {
        width: 100%;
    }
}

.card-text {
    text-align: center;
    padding: 0.5rem;

    div:first-child {
        margin-bottom: 0.5rem;
    }
}


</style>