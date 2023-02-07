<script>
import { store } from '../store';

export default {
    name: 'SectionOne',
    data () {
        return {
            store
        }
    },
}
</script>

<template>
    <div class="section-1">
        <form action="">
            <select name="search" id="type">
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