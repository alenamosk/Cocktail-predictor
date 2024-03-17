# Cocktail Predictor

Cocktail Predictor is a small web application that provides users with cocktail recommendations. By answering a few questions, users can discover the perfect cocktail for their mood. The application fetches cocktail information, including images and details, from an api source, ensuring a diverse selection of options for users to explore.

## Project Status

Cocktail Predictor is still a work in progress. This project is primarily for studying the Vue.js framework and deepen my understanding of web development, but it's also designed to be fun! Learning is much more enjoyable when it's paired with something entertaining :)

### Features

- **Personalised Recommendations:** Users answer three questions about their age, mood and how many drinks they already had.
- **Dynamic Suggestions:** Based on the user's responses, the application generate a cocktail. Users under 18 years old will get only non-alcoholic options. Users 18+ years of age will receive cocktails based on their answers to the second question about their mood. Answer “Okay” will generate any random cocktail, “Great” - random cocktail with champagne, “I’ve been better” - random cocktail with rum, “Stressed out” - random cocktail with vodka, but if user choose answer “Who’s counting” on the third question about quantity of drinks that he have had - the application displays only non-alcoholic options.
- **Cocktail Details:** Each recommended cocktail is accompanied by its name and an enticing image.
- **API Integration:** The application integrates with an api to fetch information about a wide range of cocktails, ensuring a diverse and extensive selection for users to explore.

## Technologies Used

- **Vue.js:** A progressive JavaScript framework used for building user interfaces.

## Credits

### Data Source

- Cocktail information fetched from the TheCocktailDB API (https://www.thecocktaildb.com/api.php) (provide the link to the API)

### Stock Images

- Background image sourced from Freepik (www.freepik.com) (https://www.freepik.com/free-photo/beeautiful-landscape-with-mountain-starry-sky_44365176.htm#fromView=search&page=1&position=19&uuid=9711013a-8e91-418b-9351-14d2e49ec448)
- Front side of the cocktail card image sourced from Freepik (www.freepik.com) (https://www.freepik.com/free-vector/hand-drawn-playing-card-back-design-illustration_108833153.htm#fromView=search&page=1&position=2&uuid=fca89705-04cd-49c4-82fa-e2b2e45854f1)
