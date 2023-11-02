# test
const express = require('express');
const app = express();
const port = 3000;

// Set up a variable to track whether the button has been clicked
let buttonClicked = false;

// Generate a random word
const randomWords = ["apple", "banana", "cherry", "dog", "elephant", "frog", "giraffe", "horse", "iguana", "jacket"];
function generateRandomWord() {
    if (!buttonClicked) {
        buttonClicked = true;
        const randomIndex = Math.floor(Math.random() * randomWords.length);
        const word = randomWords[randomIndex];
        return word;
    }
    return null;
}

// Serve the HTML page
app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html');
});

// Handle button click on the server
app.get('/generate', (req, res) => {
    const word = generateRandomWord();
    res.json({ word });
});

app.listen(port, () => {
    console.log(`Server is running on port ${port}`);
});
