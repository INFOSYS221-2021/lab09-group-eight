## Members
* Devon McGrath
* Komal Jabbar
* Natasha Williams
* Jen Feng William Liang

<p>
Exercise 1 <br>
1: GET is used to request data from a specificed resource, example would be https://deckofcardsapi.com/api/deck/<<deck_id>>/draw/?count=2 which is used to draw 2 cards from a  specified deck according to their IDs which will return a response in a form of a JSON list.<br>
  2: Features: Shuffle, Draw, reshuffle, new deck, partial deck, piles, add to piles, shuffle piles, list cards, draw from piles <br>
  3: https://deckofcardsapi.com/api/deck/new/jokers_enabled=true <br>
  4:a) 2 cards are drawn, king of hearts and 8 of clubs<br>
    b) we would make our json object linked to a varible named = x and use: console.log(x.deck_id)<br>
    c) same from answer above but we call: console.log(x.cards)<br>
  
 Exercise 2 <br>
>
> // Initialise the values at the start of the game
> // Do not change this part!
> let thisDeck;
> let numOfHits = 0;
> let sum = 0;
>
> // Getting different elements from HTML
> // Do not change this part!
> const hitMeBtn = document.getElementById('hitMeBtn');
> const restartBtn = document.getElementById('restartBtn');
> const hitMeSum = document.getElementById('hitMeSum');
> const hitMeCards = document.getElementById('hitMeCards');
> hitMeBtn.addEventListener('click', playGame);
> restartBtn.addEventListener('click', restartGame);
> 
> // Complete the following TODOs for each function
>
> // This function shuffles a new deck of card
> // and returns the deck id
> async function createDeck() {
>  // TODO 1: use the appropriate API to shuffle 
>  // a new deck of card
>  let response = await fetch('https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1');
>
>  if (response.status === 200) {
>    let data = await response.json();
>
>    // TODO 2: get the id of the deck from data
>    deckID = data.deck_id;
>    return deckID;
>  }
> }
>
> // This function returns all available information
> // about a card drawn from the deck created
> async function getACard() {
>  // TODO 3: use the appropriate API to draw one card 
>  // from the deck created at the start of the game
>  // Hint: use the variable thisDeck
>  let response = await fetch('https://deckofcardsapi.com/api/deck/' + thisDeck+'/draw/?count=1');
>  
>  // retun card information
>  // Do not change this
>  if (response.status === 200) {
>    let cardInfo = await response.json();
>    return cardInfo;
>  }
> }
>
> // This function returns the appropriate value
> // based on cardInfo
> function getValueFromCard(cardInfo) {
>  // TODO 4: find the value and suit of the card
>  let cardValue = cardInfo.cards[0].value;
>  let cardSuit = cardInfo.cards[0].suit;
>  
>  // TODO 5: update the cardValue appropriately
>  // if card is Jack, then set the cardValue to 11, etc
>  if (cardValue == 'JACK') {
>    cardValue = 11;
>  } 
>  if (cardValue == 'QUEEN') {
>    cardValue = 12;
>  } 
>  if (cardValue == 'KING') {
>    cardValue = 13;
>  } 
>  if (cardValue == 'ACE') {
>    cardValue = 1;
>  } 
>  console.log(cardValue);
>  // if a card is red, then the value will be negative
>  // Do not change this.
>  let posOrNeg = 1;
>  if (cardSuit == 'DIAMONDS' || cardSuit == 'HEARTS') {
>    posOrNeg = -1;
>  }
>  
>  return cardValue * posOrNeg;
> }
>
> // This function gets the image from cardInfo
> // and updates the HTML
> function updateCardImg(cardInfo) {
>    // TODO 6: find the image of the card
>    console.log(cardInfo);
>  let imgUrl = cardInfo.cards[0].image;
>  console.log(imgUrl);
>  
>  // update HTML. Do not change this.
>  hitMeCards.innerHTML += "<img src='" + imgUrl + "' width='100' />";
> }
>
> // This function controls the flow of the game
> // Do not change this function!
> async function playGame() {
>  // get a new deck of card if we just start the game
>  if (numOfHits === 0) {
>    thisDeck = await createDeck();
>  }
>   
>  // update the number of hits and button
>  numOfHits = numOfHits + 1;
>  restartBtn.disabled = false;
>  
>  // get card information and image, and
>  // update the sum of cards
>  cardInfo = await getACard();
>  updateCardImg(cardInfo);
>  sum += getValueFromCard(cardInfo);
>  
>  // check if we have reached the end of the game, and
>  // update HTML appropriately
>  if (numOfHits > 4) {
>    hitMeSum.innerHTML = "End of Game! Total value of your cards is " + sum;
>    hitMeBtn.disabled = true;
>  } else {
>    hitMeSum.innerHTML = "Current total value of your cards is " + sum;
>  }
> }
>  hitMeSum.innerHTML = "Click Hit Me! to start playing!"
>  hitMeCards.innerHTML = "";
>}
>
</p>
