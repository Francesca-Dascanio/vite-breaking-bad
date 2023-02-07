<script>
import { store } from '../store';

export default {
    name: 'SectionOne',
    data () {
        return {
            store
        }
    },
    methods: {
        getOption: function () {

            this.store.selectedOption = document.getElementById('type').value;
            console.log(this.store.selectedOption);
            
        }
    }, 
    computed: {
        // archetypesFiltered () {
        //     console.log(this.store.cards.filter((card) => card.archetype == item));
        //     return this.store.cards.filter((card) => card.archetype == item);
        // }
    }
}
</script>

<template>
    <div class="section-1">
        <form action="">
            <select name="select" id="type" @change="getOption()">
                <option>
                    Select an option
                </option>
                <option :value="item" v-for="item in store.typesArchetypes">
                    {{ item }}
                </option>
            </select>
        </form>
    </div>

</template>

<style lang="scss" scoped>


.section-1 {
    padding: 1rem;

    select {
        padding: 0.5rem 2rem;
    }
}

</style>