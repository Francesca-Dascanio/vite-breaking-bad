<script>
import SectionOne from './SectionOne.vue';
import Card from './Card.vue';
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
    computed: {
        filteredStoreCards () {
            if (this.store.selectedOption == '') {
                return this.store.cards;
            }
            else {
                
                return this.store.cards.filter((card) => card.archetype == this.store.selectedOption);
            }
        }
    },
    created() {
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
        .then ((response) => {

            this.store.cards = response.data.data.slice(0,40);

            // Crea array di archetypes
            for (let i = 0; i < this.store.cards.length; i++) {
                this.store.allArchetypes.push(this.store.cards[i].archetype);
            }

            
            // Crea array con i tipi di archetypes
            for (let i = 0; i < this.store.allArchetypes.length; i++) {

                if (this.store.typesArchetypes.includes(this.store.allArchetypes[i])) {
                // Non succede nulla
                }
                else {
                    this.store.typesArchetypes.push(this.store.allArchetypes[i]);

                    // if (this.store.allArchetypes[i] == undefined) {
                    //     this.store.allArchetypes[i] = 'undefined';
                    // }
                    
                }
            }
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
                            Found {{ filteredStoreCards.length }} cards
                        </strong>
                    </div>

                    <div class="cards-board">
                        <!-- card singola -->
                        <div class="card" v-for="(card, index) in filteredStoreCards">
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

                width: calc((100% / 5) - 10px);
                margin-bottom: 10px;
            }

        }
    }
}

.spinner-container {
    background-color: $primary-color;
    width: 100%;
    display: flex;
    justify-content: center;

    .lds-spinner {
    color: official;
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;


    div {
        transform-origin: 40px 40px;
        animation: lds-spinner 1.2s linear infinite;

        &:after {
            content: " ";
            display: block;
            position: absolute;
            top: 3px;
            left: 37px;
            width: 6px;
            height: 18px;
            border-radius: 20%;
            background: #fff;
        }

        &:nth-child(1) {
            transform: rotate(0deg);
            animation-delay: -1.1s;
        }

        &:nth-child(2) {
            transform: rotate(30deg);
            animation-delay: -1s;
        
        }

        &:nth-child(3) {
            transform: rotate(60deg);
            animation-delay: -0.9s;
        
        }

        &:nth-child(4) {
            transform: rotate(90deg);
            animation-delay: -0.8s;
        
        }

        &:nth-child(5) {
            transform: rotate(120deg);
            animation-delay: -0.7s;
        
        }

        &:nth-child(6) {
            transform: rotate(150deg);
            animation-delay: -0.6s;
        
        }

        &:nth-child(7) {
            transform: rotate(180deg);
            animation-delay: -0.5s;
        
        }

        &:nth-child(8) {
            transform: rotate(210deg);
            animation-delay: -0.4s;
        }

        &:nth-child(9) {
            transform: rotate(240deg);
            animation-delay: -0.3s;
        
        }

        &:nth-child(10) {
            transform: rotate(270deg);
            animation-delay: -0.2s;
        
        }

        &:nth-child(11) {
            transform: rotate(300deg);
            animation-delay: -0.1s;
        }

        &:nth-child(12) {
            transform: rotate(330deg);
            animation-delay: 0s;
        }

        @keyframes lds-spinner {
        0% {
            opacity: 1;
        }
        100% {
            opacity: 0;
        }
        }
    }

}

}

</style>
