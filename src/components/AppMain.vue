<script>
import SectionOne from './Main/SectionOne.vue';
import Card from './Main/Card.vue';
import axios from 'axios';
import { store } from '../store';

export default {
    name: 'AppMain',
    components: {
        SectionOne,
        Card
    },
    data () {
        return {
            store
        }
    },
    created() {
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
        .then ((response) => {

            console.log(response);
     
            this.store.cards = response.data.data.slice(0,20);
            console.log(this.store.cards);
            
        });
    }
}
</script>

<template>
    <div>
        <div class="container">
            <SectionOne/>

            <div class="section-2">
                <div class="container-internal">
                    <div class="cards-number">
                        <strong>
                            Found {{ store.cards.length }} cards
                        </strong>
                    </div>
                    <div class="cards-board">
                        <!-- card singola -->
                        <div class="card" v-for="(card, index) in store.cards">
                            <Card :card="card"/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<style lang="scss" scoped>
@use '../styles/partials/variables.scss' as *;

div {
    width: 100%;
    background-color: $primary-color;

    .container {
        max-width: 1200px;
        margin: 0 auto;
    }

}

.section-2 {
    background-color: $secondary-color;

    .container-internal {
        max-width: 1100px;
        margin: 0 auto;
        background-color: $secondary-color;
        padding: 3rem 0 1rem;

        .cards-number {
            background-color: $tertiary-color;
            color: $secondary-color;
            padding: 1rem;
        }

        .cards-board {
            background-color: $secondary-color;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;

            .card {

                width: calc((100% / 5) - 5px);
                margin-bottom: 10px;
            }

        }
    }
}

</style>
