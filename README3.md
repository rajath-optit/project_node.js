Creating a RESTful API with Express.js involves setting up routes to handle different HTTP methods (GET, POST, PUT, DELETE) and interacting with a database for data exchange. Below is a simple example to get you started. Ensure you have Node.js and npm installed on your system.

Initialize your project:

bash
Copy code
mkdir express-api
cd express-api
npm init -y
Install Express and other dependencies:

bash
Copy code
npm install express mongoose body-parser
express: Web framework for Node.js
mongoose: MongoDB object modeling tool
body-parser: Middleware to parse JSON and url-encoded data
Create your main file, e.g., index.js:

javascript
Copy code
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();
const port = process.env.PORT || 3000;

// Connect to MongoDB (Make sure you have MongoDB installed and running)
mongoose.connect('mongodb://localhost:27017/your-database-name', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

// Define a simple mongoose schema and model
const itemSchema = new mongoose.Schema({
  name: String,
  description: String
});

const Item = mongoose.model('Item', itemSchema);

// Middleware to parse JSON and url-encoded data
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// Define routes
app.get('/api/items', async (req, res) => {
  try {
    const items = await Item.find();
    res.json(items);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.post('/api/items', async (req, res) => {
  try {
    const newItem = new Item(req.body);
    const savedItem = await newItem.save();
    res.json(savedItem);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.get('/api/items/:id', async (req, res) => {
  try {
    const item = await Item.findById(req.params.id);
    res.json(item);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.put('/api/items/:id', async (req, res) => {
  try {
    const updatedItem = await Item.findByIdAndUpdate(req.params.id, req.body, { new: true });
    res.json(updatedItem);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.delete('/api/items/:id', async (req, res) => {
  try {
    const deletedItem = await Item.findByIdAndDelete(req.params.id);
    res.json(deletedItem);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
Run your application:

bash
Copy code
node index.js
Your RESTful API should now be running on http://localhost:3000. You can use tools like Postman or cURL to test the API endpoints.

Remember to replace 'mongodb://localhost:27017/your-database-name' with the actual connection string for your MongoDB instance. Also, make sure to handle security aspects such as input validation, error handling, authentication, and authorization based on your application requirements.
