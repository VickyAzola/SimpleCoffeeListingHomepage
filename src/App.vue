<script setup>
import { ref, onMounted, computed } from 'vue'
import Card from './components/Card.vue';

const selected = ref(0)
const coffeeList = ref([])

function handleClick(index) {
  selected.value = index
}

onMounted(() => {
  fetch('https://raw.githubusercontent.com/devchallenges-io/web-project-ideas/main/front-end-projects/data/simple-coffee-listing-data.json')
    .then(response => response.json())
    .then(data => {
      coffeeList.value = data
    })
    .catch(error => {
      console.log(error)
    })
})

const filteredCoffeeList = computed(() => {
  if (selected.value === 0) {
    return coffeeList.value
  } else if (selected.value === 1) {
    return coffeeList.value.filter(coffee => coffee.available)
  }
})

</script>

<template>
  <main>
    <section class="cards-container">
      <div class="top-section">
        <h1>Our Collection</h1>
        <p>Introducing our Coffee Collection, a selection of unique coffees 
          from different roast types and origins, 
          expertly roasted in small batches and shipped fresh weekly.
        </p>

        <div class="buttons">
          <button 
            @click="handleClick(0)" 
            :class="selected === 0 ? 'buttonActive' : 'buttonInactive'"
          >
            All Products
          </button>
          <button 
            @click="handleClick(1)" 
            :class="selected === 1 ? 'buttonActive' : 'buttonInactive'"
            >
              Available Now
            </button>
        </div>
      </div>

      <Card class="allCards" :coffeeList="filteredCoffeeList"/>
    </section>
  </main>
</template>

<style scoped>
.cards-container {
  background-color: #1B1D1F;
  width: 25rem;
  margin: 7rem 0 5rem;
  border-radius: .8rem;
  padding-bottom: 3rem;
}

.top-section {
  padding: 2rem 1rem;
  text-align: center;
  background-image: url('/vector.svg');
  background-repeat: no-repeat;
  background-position: top 20% right -3.8rem;
  overflow: hidden;
}

h1 {
  color: #FEF7EE;
  font-size: 3rem;
  padding-top: 2rem;
  margin-bottom: .5rem;
}

p {
  color: #6F757C;
  font-size: 1rem;
  max-width: 19.5rem;
  margin-inline: auto;
}

.buttons {
  display: flex;
  justify-content: center;
  column-gap: .5rem;
  margin-top: 1rem;
}

.buttons .buttonInactive {
  font-weight: bold;
  background-color: transparent;
  color: #FEF7EE;
  border: none;
  border-radius: .4rem;
  padding: .5rem 1rem;
}

.buttons .buttonActive {
  font-weight: bold;
  background-color: #6F757C;
  color: #FEF7EE;
  border: none;
  border-radius: .4rem;
  padding: .5rem 1rem;
}

button:hover {
  cursor: pointer;
}

.allCards {
  display: grid;
  row-gap: 3rem;
}

@media (750px <= width) {
  .cards-container {
    width: 42rem;
  }
  .top-section {
    max-width: 30rem;
    margin-inline: auto;
    background-position: top 20% right 2rem;
  }
  p {
    max-width: 28rem;
  }
  .allCards {
    grid-template-columns: 1fr 1fr;
    max-width: max-content;
    margin-inline: auto;
    column-gap: 2rem;
  }
}

@media (width >= 1024px) {
  .cards-container {
    width: 62rem;
  }
  .allCards {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
</style>

