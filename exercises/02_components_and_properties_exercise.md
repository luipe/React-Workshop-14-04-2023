## Exercise 2 - Memory Game Field
Goal: We implement a simple Memory game in several steps. The first exercise for this Memory game will build the field with cards.


### Steps
1. Create a component **`Card`**, which displays the static text *Card*, and include this **`Card`** component in `App.tsx`
   * You could use or extend the following css as style:
    ```css
    .Card {
        width: 200px;
        height: 200px;
        border: 1px solid black;
     }
    ```
2. Extend the **`Card`** component, so that the card's text is injected as a prop
3. Adjust the `App` so that 8  cards are shown which display the text *Card 1* to *Card 8*
   * *Try using `.map` on a suitable array, to avoid code duplication*
   * *Use this snippet to create a JS-array from 1 to 8:*
    ```js
    const arr = Array(8).fill().map((_, i) => i + 1);
    ```
4. Extract the displaying of the cards into a separate component **`Field`**
   * Above the field of cards, display as headline (`h1`) the name of the game
   * You could use a `display: flex` as css for the Field