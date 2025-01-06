// Import necessary dependencies
const express = require('express');
const cors = require('cors');

const app = express();

// Use CORS middleware
app.use(cors({
    origin: '*', // Allow all origins. Replace '*' with your frontend URL or app if needed.
    methods: ['GET', 'POST'], // Specify allowed HTTP methods.
    allowedHeaders: ['Content-Type', 'Authorization'], // Specify allowed headers.
}));

// Middleware to parse JSON
app.use(express.json());

// Endpoint for handling location data
app.post('/location', (req, res) => {
    const { latitude, longitude } = req.body;

    // Validate incoming data
    if (latitude === undefined || longitude === undefined) {
        return res.status(400).json({ error: "Latitude and Longitude are required" });
    }

    console.log(`Received location data: Latitude ${latitude}, Longitude ${longitude}`);
    res.status(200).send('Location data received successfully');
});

// Start the server
const port = 3000;
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});

// Default route
app.get('/', (req, res) => {
    res.send('Welcome to My Project Backend!');
});
