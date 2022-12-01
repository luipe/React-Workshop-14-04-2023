## Exercise 3 - Memory Game Interactions

**Goal:** We continue building our memory game by making the memory cards from the previous exercise interactive.

### Task
With the help of `useState()` and the `onClick` event handler, implement turning of cards such that:

* Memory cards do not show their text initially.
* When a card is clicked, the card is revealed (its text is displayed).
* When the card is clicked again, the text on the card is hidden again.

**Hint:** Instead of giving each card its own state, organize the state in the `Field` component.
Each card can retrieve the relevant part of the state and a callback function for the state update as `props`.
This will enable you to later add logic that requires knowledge about the state of multiple cards at the same time.

### Bonus exercise
If you have finished the first part, have some time left and want to add more game logic, these could be your next steps:

1. Produce (random) pairs of matching cards.
2. Ensure that only two cards can be revealed at the same time.
   1. Clicking on a revealed card has no effect.
   2. Clicking on a third (hidden) card does not reveal that card, but hides both cards that are already revealed.
3. Revealed matching pairs stay open.
4. Make the found pairs distinguishable from the rest of the cards, or let them disappear completely.
5. When all matching pairs are revealed, a button is shown that starts a new game.