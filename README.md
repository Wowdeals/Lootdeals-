<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LootDeals</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Welcome to LootDeals</h1>
    </header>
    <main>
        <!-- Deal listings will be dynamically generated here -->
    </main>
    <footer>
        <!-- Footer content here -->
    </footer>
    <script src="script.js"></script>
</body>
</html>// Your backend server code (server.js)
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(express.static('public'));

// Sample deals data
const deals = [
    {
        title: "50% off on Electronics!",
        description: "Get amazing deals on electronics items today only.",
        link: "https://example.com/electronics-deals"
    },
    // Add more deals here
];

// Route to fetch deals
app.get('/api/deals', (req, res) => {
    res.json(deals);
});

// Start server
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

// Your frontend JavaScript code (script.js)
window.onload = async () => {
    try {
        const response = await fetch('/api/deals');
        const deals = await response.json();
        displayDeals(deals);
    } catch (error) {
        console.error('Error fetching deals:', error);
    }
};

function displayDeals(deals) {
    const mainElement = document.querySelector('main');
    deals.forEach(deal => {
        const dealElement = document.createElement('div');
        dealElement.classList.add('deal');
        dealElement.innerHTML = `
            <h2>${deal.title}</h2>
            <p>${deal.description}</p>
            <a href="${deal.link}" target="_blank">View Deal</a>
        `;
        mainElement.appendChild(dealElement);
    });
}
