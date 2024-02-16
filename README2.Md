step 1:
have Node.js and npm (Node Package Manager) installed on your machine.

Initialize your project:

Open your terminal and run the following commands:

bash
Copy code
mkdir blogging-platform
cd blogging-platform
npm init -y
This will create a package.json file with default values.

Install necessary dependencies:

Install Express.js, EJS (a template engine for rendering HTML), and Body-parser (middleware to handle HTTP post requests):

bash
Copy code
npm install express ejs body-parser
Create your server file (app.js):

Create an app.js file and set up your Express server:

javascript
Copy code
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const port = 3000;

app.use(bodyParser.urlencoded({ extended: true }));
app.set('view engine', 'ejs');

// Routes
app.get('/', (req, res) => {
    // Display a list of blog posts
    res.render('index');
});

app.get('/post/:id', (req, res) => {
    // Display a single blog post based on ID
    const postId = req.params.id;
    res.render('post', { postId });
});

app.post('/create', (req, res) => {
    // Create a new blog post
    const { title, content } = req.body;
    // Add logic to store the blog post data (e.g., in a database)
    res.redirect('/');
});

// Start the server
app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
Create views (views/index.ejs, views/post.ejs):

Create two EJS files in a views folder: index.ejs and post.ejs.

views/index.ejs:

html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blogging Platform</title>
</head>
<body>
    <h1>Welcome to the Blogging Platform</h1>
    <!-- Display a list of blog posts -->
    <ul>
        <!-- Add logic to dynamically generate list items based on stored posts -->
        <li><a href="/post/1">Sample Post 1</a></li>
        <li><a href="/post/2">Sample Post 2</a></li>
    </ul>
</body>
</html>
views/post.ejs:

html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= postId %> - Blogging Platform</title>
</head>
<body>
    <h1>Post <%= postId %></h1>
    <!-- Add logic to display the content of the selected post -->
    <p>Sample content for post <%= postId %></p>
</body>
</html>
Run your application:

In the terminal, run:

bash
Copy code
node app.js
Visit http://localhost:3000 in your browser to see the blogging platform in action.

