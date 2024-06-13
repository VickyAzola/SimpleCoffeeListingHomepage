<script setup>
import FilledStar from '/Star_fill.svg'
import UnfilledStar from '/Star.svg'

const props = defineProps({
    coffeeList: {
        type: Array,
        required: true
    }
})

</script>

<template>
    <section>
        <div class="card" v-for="coffee in coffeeList" :key="coffee.id">
            <img class="cafe-img" :src="coffee.image" alt="Coffee Image">
            <p class="popular" v-if="coffee.popular">Popular</p>
            <div>
                <div class="namePrice">
                    <h2>{{ coffee.name }}</h2>
                    <p class="price">{{ coffee.price }}</p>
                </div>
                <div class="bottom-section">
                    <div class="stats">
                        <img v-if="coffee.rating" :src=FilledStar alt="filled star">
                        <img v-else :src=UnfilledStar alt="unfilled star">
                        <p class="rating" v-if="coffee.rating">{{ coffee.rating }}  <span>({{ coffee.votes }} votes)</span></p>
                        <p class="noRatings" v-else>No ratings</p>
                    </div>
                    <p class="soldOut" v-if="!coffee.available">Sold out</p>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>

.card {
    position: relative;
    width: 16rem;
    margin-inline: auto;
}

.cafe-img {
    width: 16rem;
    border-radius: .8rem;
}

.popular {
    position: absolute;
    padding: .25rem .7rem;
    background-color: #F6C768;
    color: #111315;
    border-radius: 2rem;
    top: .5rem;
    left: .5rem;
    font-size: 0.625rem;
    font-weight: bold;
}

.namePrice {
    display: flex;
    column-gap: .5rem;
    align-items: center;
    justify-content: space-between;
    font-size: 0.75rem;
    margin: .5rem 0;
}

h2 {
    font-size:  0.875rem;
}

h2, .rating  {
    color: #FEF7EE;
}

.price {
    background-color: #BEE3CC;
    padding: .2rem .5rem;
    border-radius: .2rem;
    font-weight: bold;
}

.bottom-section {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.rating span {
    color: #6F757C;
}

.noRatings {
    color: #6F757C;
}

.stats {
    display: flex;
    column-gap: .2rem;
    align-items: center;
    font-size: 0.875rem;
    margin-bottom: .5rem;
}

.soldOut {
    color: #ED735D;
}

</style>