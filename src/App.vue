<template>
  <div id="app">
    <main>
      <div class="greetings-box">
        <h1>Welcome to Cocktail Predictor</h1>
        <h3>If you don't know what to drink, then get ready!</h3>
        <h3>Cocktail predictor will choose the best option for you</h3>
        <h1>🔮</h1>
      </div>

      <div class="main-content">
        <div class="questionnaire">
          <h2 class="title">
            First, you need to fill out a short questionnaire
          </h2>

          <div class="questions">
            <p>How old are you?</p>

            <input type="radio" id="under18" value="Under18" v-model="age" />
            <label for="one">Under 18</label><br />

            <input type="radio" id="over18" value="Over18" v-model="age" />
            <label for="two">18+</label>
          </div>

          <div class="questions">
            <p>How are you today?</p>

            <input type="radio" id="okay" value="Okay" v-model="mood" />
            <label for="one">Okay</label><br />

            <input type="radio" id="great" value="Great" v-model="mood" />
            <label for="two">Great</label><br />

            <input
              type="radio"
              id="been-better"
              value="Been-better"
              v-model="mood"
            />
            <label for="two">I've been better</label><br />

            <input type="radio" id="stressed" value="Stressed" v-model="mood" />
            <label for="two">Stressed out</label><br />
          </div>

          <div class="questions">
            <p>How much drinks have you had already?</p>

            <input type="radio" id="zero-two" value="1-2" v-model="drinks" />
            <label for="one">0-2</label><br />

            <input type="radio" id="three-four" value="3-4" v-model="drinks" />
            <label for="two">3-4</label><br />

            <input
              type="radio"
              id="counting"
              value="How-is-counting"
              v-model="drinks"
            />
            <label for="two">How's counting?</label>
          </div>

          <button id="button" @click="flipCard">Give me a cocktail!</button>

          <div v-if="errorMessage" class="error-message">
            {{ errorMessage }}
          </div>
        </div>

        <div class="flip-box" :class="{ hovered: cocktail }">
          <div class="flip-card-wrap">
            <div class="card-box-front">
              <img
                class="card-front-side"
                src="./assets/card-back-side.PNG"
                height="400px"
                width="350px"
              />
            </div>

            <div class="cocktail-box-back" v-if="cocktail">
              <p>This is your cocktail for today</p>
              <h2>"{{ cocktail.name }}"</h2>
              <img
                class="cocktail-img"
                :src="cocktail.image"
                :alt="cocktail.name"
                height="350px"
                width="350px"
              />
            </div>
          </div>
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
      errorMessage: "",
    };
  },
  methods: {
    flipCard() {
      if (!this.age || !this.mood || !this.drinks) {
        this.errorMessage =
          "Please answer all questions before getting a cocktail.";
        return;
      }
      this.fetchCocktail();
    },
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
        if (this.age === "Over18" && this.drinks === "How-is-counting") {
          url = this.url_base_non_alcoholic;
        }
        const response = await fetch(url);
        const data = await response.json();

        this.errorMessage = "";

        if (data.drinks && data.drinks.length > 0) {
          let randomIndex = Math.floor(Math.random() * data.drinks.length);
          const cocktailData = data.drinks[randomIndex];

          const cocktailName = cocktailData.strDrink;
          const image = cocktailData.strDrinkThumb;

          const cocktailInfo = {
            name: cocktailName,
            image: image,
          };

          this.cocktail = cocktailInfo;

          document.querySelector(".flip-box").classList.add("hovered");
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
* {
  box-sizing: border-box;
}

body {
  background-image: url(./assets/beeautiful-landscape-with-mountain-starry-sky.jpg);
  background-position: center;
  background-size: 100% 100%;
  background-repeat: no-repeat;
  overflow: hidden;
  overflow-y: scroll;
  display: flex;
  justify-content: center;
}

.main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-size: 5px;
  padding: 10px;
}

.main-content {
  background-color: white;
  opacity: 0.9;
  margin-left: 15px;
  margin-right: 15px;
  margin-bottom: 15px;
  padding-bottom: 20px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.greetings-box {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
  color: white;
  padding: 20px;
}

h1 {
  font-weight: bold;
  font-size: 30px;
}

.questionnaire {
  margin: 15px;
  padding: 15px;
}

h2 {
  color: black;
  font-weight: bold;
  font-size: 25px;
}

.questions,
.title {
  margin-bottom: 10px;
}

#under18,
#over18,
#okay,
#great,
#been-better,
#stressed,
#zero-two,
#three-four,
#counting {
  margin-right: 10px;
}

#button {
  background-color: #e7d3fd;
  color: black;
  font-size: 15px;
  margin-top: 10px;
  padding: 8px 16px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  text-align: center;
}

#button:hover {
  background-color: #642b6b;
  color: white;
}

.error-message {
  color: red;
  padding-top: 10px;
}

.flip-box {
  margin: 0 auto;
  display: flex;
  background-color: transparent;
  width: 350px;
  height: 400px;
  perspective: 1000px;
}

.flip-card-wrap {
  position: relative;
  width: 350px;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-box.hovered .flip-card-wrap {
  transform: rotateY(180deg);
}

.card-box-front,
.cocktail-box-back {
  position: absolute;
  width: 350px;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.card-box-front {
  color: black;
}

.cocktail-box-back {
  background-color: #e7d3fd;
  border-radius: 10px;
  transform: rotateY(180deg);
}

.cocktail-img {
  border-radius: 10px;
}

@media screen and (min-width: 480px) {
  .main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    justify-content: space-around;
    font-size: 5px;
    /* padding: 10px; */
  }
}

@media screen and (min-width: 480px) {
  .main-content {
    background-color: white;
    opacity: 0.9;
    border-radius: 30px;
    display: flex;
    flex-direction: row;
    justify-items: center;
    max-width: 1200px;
    min-width: 720px;
  }
}

@media screen and (min-width: 480px) {
  .flip-box {
    display: flex;
    background-color: transparent;
    max-width: 100%;
    height: 400px;
    margin-right: 30px;
    perspective: 1000px;
  }
}
</style>
