Creating a task management app with Node.js for the backend and React for the frontend involves several steps. Below is a basic outline to help you get started. Note that this is a simplified example, and in a real-world scenario, you might need additional features, security measures, and optimizations.

 Backend (Node.js with Express)

1. Initialize Node.js Project:
   ```
   mkdir task-management-app
   cd task-management-app
   npm init -y
   ```

2. Install Dependencies:
   ```
   npm install express mongoose body-parser cors
   ```

3. Set Up Express Server (server.js):
   ```javascript
   const express = require('express');
   const mongoose = require('mongoose');
   const bodyParser = require('body-parser');
   const cors = require('cors');

   const app = express();
   const PORT = process.env.PORT || 5000;

   // Middleware
   app.use(bodyParser.json());
   app.use(cors());

   // MongoDB Connection
   mongoose.connect('mongodb://localhost/task_management', {
     useNewUrlParser: true,
     useUnifiedTopology: true,
   });

   const db = mongoose.connection;
   db.on('error', console.error.bind(console, 'MongoDB connection error:'));
   db.once('open', () => {
     console.log('Connected to MongoDB');
   });

   // Routes (to be defined)

   // Start Server
   app.listen(PORT, () => {
     console.log(`Server is running on http://localhost:${PORT}`);
   });
   ```

4. Define Task Model (models/Task.js):
   ```javascript
   const mongoose = require('mongoose');

   const taskSchema = new mongoose.Schema({
     title: { type: String, required: true },
     description: String,
     completed: { type: Boolean, default: false },
   });

   module.exports = mongoose.model('Task', taskSchema);
   ```

5. Create Routes (routes/tasks.js):
   ```javascript
   const express = require('express');
   const router = express.Router();
   const Task = require('../models/Task');

   // Define routes (CRUD operations)

   module.exports = router;
   ```

6. Implement CRUD Operations in Routes (routes/tasks.js):
   ```javascript
   // Import necessary modules and define CRUD operations

   router.get('/', async (req, res) => {
     // Fetch all tasks from the database
   });

   router.post('/', async (req, res) => {
     // Create a new task in the database
   });

   router.put('/:id', async (req, res) => {
     // Update a task in the database
   });

   router.delete('/:id', async (req, res) => {
