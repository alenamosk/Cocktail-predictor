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

        <input type="radio" id="under18" value="Under18" v-model="picked" />
        <label for="one">Under 18 years of age</label>

        <input type="radio" id="over18" value="Over18" v-model="picked" />
        <label for="two">Over 18 years of age</label>

        <div>How are you today?</div>

        <input type="radio" id="okay" value="Okay" v-model="picked" />
        <label for="one">Okay</label>

        <input type="radio" id="great" value="Great" v-model="picked" />
        <label for="two">Great</label>

        <input
          type="radio"
          id="been-better"
          value="Been-better"
          v-model="picked"
        />
        <label for="two">I've been better</label>

        <input type="radio" id="stressed" value="Stressed" v-model="picked" />
        <label for="two">Stressed out</label>

        <div>How much drinks have you had already?</div>

        <input type="radio" id="under18" value="Under18" v-model="picked" />
        <label for="one">1-2</label>

        <input type="radio" id="over18" value="Over18" v-model="picked" />
        <label for="two">3-4</label>

        <input type="radio" id="over18" value="Over18" v-model="picked" />
        <label for="two">How's counting?</label>
      </div>

      <div class="card-wrap">
        <div class="card-box">
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
          <img src="./assets/card-back-side.PNG" height="350px" width="350px" />
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
      api_key: "1",
    };
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
