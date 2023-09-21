<template>
    <div class="wrapper">
        <div class="content">
            <div class="personen">
                <span>Aantal personen</span>
                <input type="number" v-model="personcount">
            </div>
            <div class="producten">
                <template v-for="item in products">
                    <span>Kcal per 100</span>
                    <input type="number" v-model="item.kcal">
                    <span>Hoeveelheid</span>
                    <input type="number" v-model="item.amount">
                </template>
            </div>
            <div class="total">
                <b>Aantal kcal per persoon:</b>
                <span>{{ count }}</span>
            </div>
        </div>
    </div>
</template>

<style>
html, body {
    margin: 0;
    padding: 0;
}

.wrapper {
    display: grid;
    place-items: center;
    min-height: 100vh;
}

.personen {
    display: grid;
    grid-template-columns: 1fr 100px;
    gap: 10px;
}

.producten {
    display: grid;
    grid-template-columns: auto 1fr auto 1fr;
    align-items: center;
    gap: 10px;
    margin: 10px 0;
}

.total {
    display: grid;
    grid-template-columns: 1fr auto;
}
</style>
<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
    data: () => ({
        personcount: 2,
        products: [{
            kcal: 100,
            amount: 350,
        }]
    }),
    computed: {
        count() {
            return new Intl.NumberFormat('nl-NL', {
                maximumFractionDigits: 2,
                minimumFractionDigits: 0,
            }).format(this.products.reduce((a, b) => a + (b.kcal * b.amount / 100), 0) / this.personcount);
        }
    }
});
</script>