<template>
  <div id="app">
    <main>
      <div class="centered-wrapper">
        <div class="greetings-box">
          <h1>🔮</h1>
          <h1>Welcome to Cocktail Predictor</h1>
          <p>If you don't know what to drink, then get ready!</p>
          <p>Cocktail predictor will choose the best options for you</p>
          <button>Start the magic</button>
        </div>
      </div>

      <div>
        <h2>I have just a few questions for you</h2>

        <div>How old are you?</div>

        <input type="radio" id="under18" value="Under18" v-model="age" />
        <label for="one">Under 18 years of age</label>

        <input type="radio" id="over18" value="Over18" v-model="age" />
        <label for="two">Over 18 years of age</label>

        <div>How are you today?</div>

        <input type="radio" id="okay" value="Okay" v-model="mood" />
        <label for="one">Okay</label>

        <input type="radio" id="great" value="Great" v-model="mood" />
        <label for="two">Great</label>

        <input
          type="radio"
          id="been-better"
          value="Been-better"
          v-model="mood"
        />
        <label for="two">I've been better</label>

        <input type="radio" id="stressed" value="Stressed" v-model="mood" />
        <label for="two">Stressed out</label>

        <div>How much drinks have you had already?</div>

        <input type="radio" id="oneTwo" value="1-2" v-model="drinks" />
        <label for="one">1-2</label>

        <input type="radio" id="threeFour" value="3-4" v-model="drinks" />
        <label for="two">3-4</label>

        <input
          type="radio"
          id="counting"
          value="How-is-counting"
          v-model="drinks"
        />
        <label for="two">How's counting?</label>

        <button @click="fetchCocktail">Get me cocktails!</button>
      </div>

      <div class="card-wrap">
        <div class="card-box">
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
        </div>
        <div class="cocktail-box" v-if="cocktail">
          <img
            :src="cocktail.image"
            :alt="cocktail.name"
            height="350px"
            width="350px"
          />
          <h2>{{ cocktail.name }}</h2>
          <p v-for="(ingredient, index) in cocktail.ingredients" :key="index">
            {{ cocktail.measures[index] }} {{ ingredient }}
          </p>
          <p>{{ cocktail.instructions }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      age: null,
      mood: null,
      drinks: null,
      cocktail: null,
      url_base: "https://www.thecocktaildb.com/api/json/v1/1/random.php",
      url_base_non_alcoholic:
        "https://www.thecocktaildb.com/api/json/v1/1/filter.php?a=Non_Alcoholic",
      url_base_champagne:
        "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=champagne",
      url_base_rum:
        "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=rum",
      url_base_vodka:
        "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=vodka",
    };
  },
  methods: {
    async fetchCocktail() {
      try {
        let url = this.url_base;
        if (this.age === "Under18") {
          url = this.url_base_non_alcoholic;
        }
        if (this.age === "Over18" && this.mood === "Great") {
          url = this.url_base_champagne;
        }
        if (this.age === "Over18" && this.mood === "Been-better") {
          url = this.url_base_rum;
        }
        if (this.age === "Over18" && this.mood === "Stressed") {
          url = this.url_base_vodka;
        }
        if (
          (this.age === "Over18" && this.mood === "Okay",
          "Great",
          "Been-better",
          "Stressed" && this.drinks === "How-is-counting")
        ) {
          url = this.url_base_non_alcoholic;
        }
        const response = await fetch(url);
        const data = await response.json();

        if (data.drinks && data.drinks.length > 0) {
          let randomIndex = Math.floor(Math.random() * data.drinks.length);
          const cocktailData = data.drinks[randomIndex];

          const cocktailName = cocktailData.strDrink;
          const ingredients = [];
          const measures = [];
          for (let i = 1; i <= 15; i++) {
            const ingredient = cocktailData[`strIngredient${i}`];
            const measure = cocktailData[`strMeasure${i}`];
            if (ingredient && measure) {
              ingredients.push(ingredient);
              measures.push(measure);
            }
          }
          const instructions = cocktailData.strInstructions;
          const image = cocktailData.strDrinkThumb;

          const cocktailInfo = {
            name: cocktailName,
            ingredients: ingredients,
            measures: measures,
            instructions: instructions,
            image: image,
          };

          this.cocktail = cocktailInfo;
        } else {
          console.error("No cocktail data found in response.");
        }
      } catch (error) {
        console.error("Error fetching cocktail:", error);
      }
    },
  },
};
</script>

<style>
#app {
}

main {
  min-height: 100vh;
  padding: 25px;
}

.card {
  height: 100px;
}

.centered-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.greetings-box {
  text-align: center;
}

h1 {
}
</style>
