<script>
import axios from 'axios';
import { store } from '../store';

export default {
    name: 'AppMain',
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
            <div class="section-1">
                <form action="">
                    <select name="" id="type">
                        <option value="alien">
                            Alien
                        </option>
                    </select>
                </form>
            </div>
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
                            <div class="card-image">
                                <img :src="card.card_images[0].image_url" alt="card-1">
                            </div>
                            <div class="card-text">
                                <div>
                                    {{ card.name }}
                                </div>
                                <div>
                                    {{ card.archetype }}
                                </div>
                            </div>
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

.section-1 {
    padding: 1rem;

    select {
        padding: 0.5rem 2rem;
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
                }
            }
        }
    }
}

</style>
