# JavaScriptCodingAssessment
// code for html

<!DOCTYPE html>
<html>
<head>
  <title>Quote Filter</title>
</head>
<body>
  <h1>Quote Filter</h1>
  <input type="text" id="searchInput" placeholder="Enter search keyword">
  <ul id="quoteList"></ul>

  <script src="script.js"></script>
</body>
</html>

***********************************************************
// code for javaScript

const quoteList = document.getElementById('quoteList');
const searchInput = document.getElementById('searchInput');
let quotes = [];

// Fetch quote data from the API
fetch('https://dummyjson.com/quotes')
  .then(response => response.json())
  .then(data => {
    quotes = data;
    displayQuotes(quotes);
  })
  .catch(error => console.error('Error:', error));

// Display quotes in the list
function displayQuotes(quotes) {
  quoteList.innerHTML = '';

  quotes.forEach(quote => {
    const li = document.createElement('li');
    li.textContent = quote.text;
    quoteList.appendChild(li);
  });
}

// Filter quotes based on user input
searchInput.addEventListener('input', () => {
  const searchKeyword = searchInput.value.toLowerCase();
  const filteredQuotes = quotes.filter(quote => quote.text.toLowerCase().includes(searchKeyword));
  displayQuotes(filteredQuotes);
});

