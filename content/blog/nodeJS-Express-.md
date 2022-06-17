---
title: "nodeJS-Express-"
date: 2022-06-07
lastmod: 2022-06-07
draft: false
blog_tags: ["nodejs"]
summary: " "
status: "nodejs"
---


# NodeJS -- Using of Express -- 

***

</br>
</br>
</br>

In this blog we want to make a small project using diffrent Libraries.

 !!  To continue with this blog, you must have a background on :
 <ul>
   <li> 
      <a href="https://youtu.be/qoSksQ4s_hg"> basics -JS-  </a>
    </li>
    <li> 
      <a href="https://youtu.be/uq7omoxwA7A"> Library -JS- </a>
    </li>
    <li> 
      <a href="https://youtu.be/DHvZLI7Db8E"> Promise </a>
    </li>
    <li> 
      <a href="https://youtu.be/1PnVor36_40" > CSS </a>
    </li>
   <li> 
      <a href="https://youtu.be/dD2EISBDjWM" > HTML </a>
    </li>
  </ul>
  
  ## Overview :

We will clarify a few things :

1- Node.js Basics;

2- Clients & Servers;

3- Req & Res;

4- NPM;

5- Express Apps;

6- View Engine;

7- Middleware;

8- MongoDB;

9- Get,Post & Delete Req;

10- Express Router & MVC;

***


### Details:
***

</br>
</br>

**1- Node.js Basics:**

- To run a Nodejs file, simply creating `*node -fileName.js-*` in cmd.

- Module & Req :


people.js : 

```javascript

const people = ['omar','mhamad','baraa','yassin'];

const age = ['5','6','10','20'];

console.log(people);

module.exports = {
    people: people,
    age : age
};

```

module.js :

```javascript

const x = require('./people');

console.log(x.people, x.age);
```
***

the Result:

```
['omar','mhamad','baraa','yassin'] ['5','6','10','20']

```

</br>

---
---

</br>

- **File Sys** : 

```javascript
const fs = require("fs");

```

</br>
---

File Tree :

{{< mermaid >}}
graph TD
    A[file] --> |file| B[assets]
    A --> |JS| C[file.js]
    A --> |txt| D[test1.txt]
    A -->|txt| E[test2.txt]
    A -->|txt| F[test3.txt]
{{</ mermaid >}}

---

-- Read File:

```javascript


fs.readFile('./test1.txt', (err,data) => {
if(err) console.error(err);
console.log(data.toString());
})


```

</br>

-- Write File:


```javascript

// if the file isn't exist , it make it.

fs.writeFile('./test1.txt', 'test2', () => {
    console.log("file has Written");
})

```


</br>

-- Directories File:


```javascript

if (!fs.existsSync("./assets"))
  
  //    if folder doesn't exist, make one
  fs.mkdir("./assets", (err) => {
    if (err) console.error(err);
    console.log("file was Maked");
  });
else {
  
  // if folder is exist then remove it. 
  fs.rmdir("./assets", (err) => {
    if (err) console.error(err);
    console.log("Folder was deeted");
  });
}

```

</br>

-- Deleting File:


```javascript

if(fs.existsSync('./assets/deleteMe.txt')){
    fs.unlink('./assets/deleteMe.txt', (err) => {
        if(err) console.error(err);
        console.log(" file was Deleted ");
    })
}

```

</br>

-- Stream & Buffer :

`Stream : Start using data  before it has finished loading`

```javascript

    const readStream = fs.createReadStream('./test2.txt',{ encoding: 'utf-8'})   
    
    // encoding: utf-8 ....like....> data.toString()

    const writeStream = fs.createWriteStream('./test3.txt');

    // readStream.on('data', (chunk)=>{
    //     console.log('---- CHUNK ----');
    //     console.log(chunk);  // without .toString , because we write an encoding above 
    //     writeStream.write('\nNew ChUNK\n');
    //     writeStream.write(chunk);
    // })


    // we can do this instead of the above code 

    readStream.pipe(writeStream);
```

</br>
</br>


**2- Clients & Servers**:

<img src="../Req.png" alt="Req-icon" style="max-width: 700px; max-height:500px;">

- Creating a server:

```javascript 

const http = require('http');

const server = http.createServer((req,res) => {
    console.log('request mode');
});

server,listen(3000,'localhost', () => {
    console.log('listening for request on port 3000');
});

```
</br>
</br>


**3- Request & Response**:

- Req & Res Object , And returning html page :

```javascript 

const server = http.createServer((req,res)=>{

    // - request object: 
    console.log(req.url,req.method);

    
    // - response object:

    res.setHeader('Content-Type','text/html');

    res.write('<head><link rel="styleset" href="#"></head>');
    res.write('<p> Hello world </p>');
    res.write('<p> Hello again </p>');

    res.end();

    // - Returning html page
    
    res.setHeader('Content-Type','text/html');

        // send an html file

        fs.readfile('./view/index.html',(err,data)=>{
            if(err){
                console.log(err);
                res.end();
            } else{
                // res.write(data); 
                res.end(data);
                // we can send data with this method 
                // because we have one things to send;
            }
        })

});


server,listen(3000,'localhost', () => {
    console.log('listening for request on port 3000');
});

```

- Basic Routing, Redirect & Status: 

```javascript

const server = http.createServer((req,res)=>{
    console.log(req.url, req.method);
    res.setHeader('Content-Type','text/html');

    const num = _.rand

    let path = './views/';
    switch(req.url){
        case '/': 
            path += 'index.html';
            res.statusCode= 200;
            break;
        case '/about':
            path += 'about.html';
            res.statusCode = 200;
            break;
        case '/about-me':
            res.statusCode= 301;
            res.setHeader('Location','/about'); // Redirect to about page
            res.end();
            break;
        default:
            path += '404.html';
            res.statusCode = 404;
            break;
    }


    // set Header content type 
    fs.readFile(path, (err,data)=>{
        if(err) console.error(err);
        
        res.write(data);
        res.end();
    });
});

server.listen(3004,'localhost',()=>{
    console.log('listening for request on port 3002');
});

```
</br>
</br>

**4- NPM**: -3rd party pack-


- npm install :: to install all packa of project.

- npm start :: to run the js code.

- [nodemon](https://www.npmjs.com/package/nodemon) :: is a tool that helps develop Node.js based applications by automatically restarting the node application when file changes in the directory are detected.

- In package.json, we look at the pck of project, in the **dependencies** section.


</br>
</br>

**5- [Express](https://www.npmjs.com/package/express) Apps:**  

- npm i express 

- code :

```javascript

const express = require('express');

const app = express();

app.listen(3000);

app.get('/',(req,res)=>{
    // res.send('<p> Home page </p>');
    res.sendFile('./views/index.html',{root: __dirname});
});

app.get('/about',(req,res)=>{
    res.sendFile('./views/about.html',{root : __dirname});
});


// redirect 

app.get('/about-us',(req,res)=>{
    res.redirect('/about');
});


// 404 code page

app.use((req,res)=>{
    res.status(404).sendFile('./views/404.html',{root : __dirname});
});

```

</br>
</br>





**6- View Engines** :  -[EJS](https://ejs.co/)- Embedded Javascript Templating

</br>

<img src="./EJS.png" alt="ejs-icon" style="max-width:850px; max-height:850px;">

</br>
</br>

> we use in EJS :
>> <% code %> :: to create a JS  code and receive variable from it.   
>> <%- include("referance of js file") %>.

> Ex:     
> js :
>    ```javascript
>    app.get('/', (req, res) => {
>  const blogs = [
>    {title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sitame  consectetur'},
>
>   {title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur'},
>   {title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur'},
>  ];
>  res.render('index', { title: 'Home', blogs });
>});
>
>
> ```
>  ejs :
>
>```html   
>
>  <%- include("./partials/nav.ejs") %>
>
>  <div class="blogs content">
>   <h2>All Blogs</h2>
>
>    <% if (blogs.length > 0) { %>
>      <% blogs.forEach(blog => { %>
>        <h3 class="title"><%= blog.title %></h3>
>       <p class="snippet"><%= blog.snippet %></p>
>      <% }) %>
>   <% } else { %>
>      <p>There are no blogs to display...</p>
>
>    <% } %>
>    
> </div>
>
> ```
>
>

</br>

- index.ejs instead of index.html.

- App.js:

> we use **res.render('about', { title: 'About' });** instead of **res.sendFile('./views/about.html',{root : __dirname})**.



```javascript

const express = require('express');

// express app
const app = express();

// listen for requests
app.listen(3000);

// register view engine
app.set('view engine', 'ejs');
// app.set('views', 'myviews');

app.get('/', (req, res) => {
  const blogs = [
    {title: 'Yoshi finds eggs', snippet: 'Lorem ipsum dolor sit ame consectetur'},
    {title: 'Mario finds stars', snippet: 'Lorem ipsum dolor sit amet consectetur'},
    {title: 'How to defeat bowser', snippet: 'Lorem ipsum dolor sit amet consectetur'},
  ];
  res.render('index', { title: 'Home', blogs });
});

app.get('/about', (req, res) => {
  res.render('about', { title: 'About' });
});

app.get('/blogs/create', (req, res) => {
  res.render('create', { title: 'Create a new blog' });
});

// 404 page
app.use((req, res) => {
  res.status(404).render('404', { title: '404' });
});

```

***
</br>

> we change the html content to receive and transmit ejs code :

- index.ejs :

```html

<html lang="en">
<%- include("./partials/head.ejs") %>

<body>
  <%- include("./partials/nav.ejs") %>

  <div class="blogs content">
    <h2>All Blogs</h2>

    <% if (blogs.length > 0) { %>
      <% blogs.forEach(blog => { %>
        <h3 class="title"><%= blog.title %></h3>
        <p class="snippet"><%= blog.snippet %></p>
      <% }) %>
    <% } else { %>
      <p>There are no blogs to display...</p>
    <% } %>
    
  </div>

  <%- include("./partials/footer.ejs") %>
</body>
</html>

```

</br>

- about.ejs:

```html
<html lang="en">
<%- include("./partials/head.ejs") %>

<body>
  <%- include("./partials/nav.ejs") %>

  <div class="about content">
    <h2>About Us</h2>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a modi tenetur ut blanditiis, illum quo consectetur recusandae excepturi natus impedit rem, tempora cum fuga quae in.</p>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a modi tenetur ut blanditiis, illum quo consectetur recusandae excepturi natus impedit rem, tempora cum fuga quae in.</p>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quia quibusdam quaerat illo a modi tenetur ut blanditiis, illum quo consectetur recusandae excepturi natus impedit rem, tempora cum fuga quae in.</p>
  </div>

  <%- include("./partials/footer.ejs") %>
</body>
</html>

```
***

</br>

- 404.ejs:

```html

<html lang="en">
<%- include("./partials/head.ejs") %>

<body>
  <%- include("./partials/nav.ejs") %>

  <div class="not-found content">
    OOPS, page not found :)
  </div>

  <%- include("./partials/footer.ejs") %>
</body>
</html>


```

***

</br>

- create.ejs:

```html

<html lang="en">
<%- include("./partials/head.ejs") %>

<body>
  <%- include("./partials/nav.ejs") %>

  <div class="create-blog content">
    <form>
      <label for="title">Blog title:</label>
      <input type="text" id="title" name="title" required>
      <label for="snippet">Blog snippet:</label>
      <input type="text" id="snippet" name="snippet" required>
      <label for="body">Blog body:</label>
      <textarea id="body" name="body" required></textarea>
      <button>Submit</button>
    </form>
  </div>

  <%- include("./partials/footer.ejs") %>
</body>
</html>


```

***

</br>

- footer.ejs:

```html

<footer>
  Copyright &copy; OJZ 2022
</footer>


```

***

</br>

- head.ejs:

```html

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Ninja | <%= title %></title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Noto+Serif:wght@400;700&display=swap');
    body{
      max-width: 1200px;
      margin: 20px auto;
      padding: 0 20px;
      font-family: 'Noto Serif', serif;
      max-width: 1200px;
    }
    p, h1, h2, h3, a, ul{
      margin: 0;
      padding: 0;
      text-decoration: none;
      color: #222;
    }
    /* nav & footer styles */
    nav{
      display: flex;
      justify-content: space-between;
      margin-bottom: 60px;
      padding-bottom: 10px;
      border-bottom: 1px solid #ddd;
      text-transform: uppercase;
    }
    nav ul{
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
    }
    nav li{
      list-style-type: none;
      margin-left: 20px;
    }
    nav h1{
      font-size: 3em;
    }
    nav p, nav a{
      color: #777;
      font-weight: 300;
    }
    footer{
      color: #777;
      text-align: center;
      margin: 80px auto 20px;
    }
    h2{
      margin-bottom: 40px;
    }
    h3{
      text-transform: capitalize;
      margin-bottom: 8px;
    }
    .content{
      margin-left: 20px;
    }
    /* index styles */
    /* details styles */
    /* create styles */
    .create-blog form{
      max-width: 400px;
      margin: 0 auto;
    }
    .create-blog input,
    .create-blog textarea{
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 8px;
    }
    .create-blog label{
      display: block;
      margin-top: 24px;
    }
    textarea{
      height: 120px;
    }
    .create-blog button{
      margin-top: 20px;
      background: crimson;
      color: white;
      padding: 6px;
      border: 0;
      font-size: 1.2em;
      cursor: pointer;
    }
  </style>
</head>


```

***

</br>

- nav.ejs:

```html 

<nav>
  <div class="site-title">
    <a href="/"><h1>Blog Ninja</h1></a>
    <p>A Net Ninja Site</p>
  </div>
  <ul>
    <li><a href="/">Blogs</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/blogs/create">New Blog</a></li>
  </ul>
</nav>


```
***

</br>

**7- Middleware :**

- Code wich runs (on the server) between getting a request and sending a response.

- Ex: 

```javascript

//  Middleware   :

app.use((req,res, next)=>{
    console.log('new Request made:');
    console.log('Host : ', req.hostname);
    console.log('Path : ', req.path );
    console.log('method : ',req.method);

    // to contimue runnig this code :
    next();
});


```
The result :

```markdown
new Request made:
Host :  localhost
Path :  /about
method :  GET
```

</br>
</br>

- [Morgan](https://www.npmjs.com/package/morgan):
    HTTP request logger middleware for node.js
> Named after Dexter, a show you should not watch until completion.
>> npm i morgan

**instead of the above code**

```javascript
const morgan = require("morgan");

app.use(morgan("dev"));

```

The result : (in console)

```markdown

GET /about 304 14.975 ms - -

```

</br>

- Static:

```javascript
app.use(express.static("public"));

```

> make a 'public' file.
> make in this folder the static files, like `style.css` , img ... 

***

</br>
</br>

**8- MongoDB:**

- [mongoose](https://www.npmjs.com/package/mongoose), 
Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose supports both promises and callbacks.

- [MongoDB Atlas](https://www.mongodb.com/atlas/database),
    to view how to create and send database , [this](https://www.youtube.com/watch?v=bxsemcrY4gQ&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=9).

- now our app.js code are :

```javascript
const express = require('express');
const morgan = require('morgan');

////////////
const mongoose = require('mongoose');
const Blog = require('./models/blog');
////////////

// express app
const app = express();

////////////
// connect to mongodb & listen for requests
const dbURI = "mongodb+srv://netninja:test1234@net-ninja-tuts-del96.mongodb.net/node-tuts";

mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(result => app.listen(3000))
  .catch(err => console.log(err));
////////////


// register view engine
app.set('view engine', 'ejs');

// middleware & static files
app.use(express.static('public'));
app.use(morgan('dev'));
app.use((req, res, next) => {
  res.locals.path = req.path;
  next();
});

////////////
// mongoose & mongo tests
app.get('/add-blog', (req, res) => {
  const blog = new Blog({
    title: 'new blog',
    snippet: 'about my new blog',
    body: 'more about my new blog'
  })

  blog.save()
    .then(result => {
      res.send(result);
    })
    .catch(err => {
      console.log(err);
    });
});

app.get('/all-blogs', (req, res) => {
  Blog.find()
    .then(result => {
      res.send(result);
    })
    .catch(err => {
      console.log(err);
    });
});

app.get('/single-blog', (req, res) => {
  Blog.findById('5ea99b49b8531f40c0fde689')
    .then(result => {
      res.send(result);
    })
    .catch(err => {
      console.log(err);
    });
});

////////////

app.get('/', (req, res) => {
  res.redirect('/blogs');
});

app.get('/about', (req, res) => {
  res.render('about', { title: 'About' });
});

////////////

// blog routes
app.get('/blogs/create', (req, res) => {
  res.render('create', { title: 'Create a new blog' });
});

app.get('/blogs', (req, res) => {
  Blog.find().sort({ createdAt: -1 })
    .then(result => {
      res.render('index', { blogs: result, title: 'All blogs' });
    })
    .catch(err => {
      console.log(err);
    });
});
////////////


// 404 page
app.use((req, res) => {
  res.status(404).render('404', { title: '404' });
});

```

</br>

- we make a new folder 'models' , include `blogs.js`.

Code :

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const blogSchema = new Schema({
  title: {
    type: String,
    required: true,
  },
  snippet: {
    type: String,
    required: true,
  },
  body: {
    type: String,
    required: true
  },
}, { timestamps: true });

const Blog = mongoose.model('Blog', blogSchema);
module.exports = Blog;


```

***

</br>
</br>

**9- Get,Post & Delete Req:**

>
>>Get : Request to get a resource.
>
>>Post : Request to create new data (new blog).
>
>>Delete : Requests to delete data (del blog).
>
>>Put : Request to update data (update a blog).
>



- create.ejs : to create new blog (form) :

Code: 

```html

<!DOCTYPE html>
<html lang="en">
    <%- include('../partials/head.ejs')%>    
<body>
    <%- include('../partials/nav.ejs')%>

        <form action="/blogs" method="post">
            <label for="title">Blog title : </label>
            <input type="text" id="title" name="title" required>
            <label for="snippet">Blog snippet : </label>
            <input type="text" id="snippet" name="snippet" required>
            <label for="body">Blog body : </label>
            <textarea id="body" name="body" required></textarea>
            <button>Submit</button>
        </form>

    <%- include('../partials/footer.ejs')%>
</body>
</html>

```

</br>

- add post blog to app.js:

Code:

```javascript

app.post('/blogs', (req, res) => {
  // console.log(req.body);
  const blog = new Blog(req.body);

  blog.save()
    .then(result => {
      res.redirect('/blogs');
    })
    .catch(err => {
      console.log(err);
    });
});


// To read and delete each data from blog

app.get("/blogs/:myid", (req, res) => {
  const id = req.params.myid;

  Blog.findById(id)
    .then(result => {
      res.render('details', { blog: result, title: "Blog Details" });
    })
    .catch((err) => console.log(err));
});



app.delete("/blogs/:myid", (req, res) => {
  const id = req.params.myid;

  Blog.findByIdAndDelete(id)
    .then((result) => {
      res.json({ redirect: "/blogs" });
    })
    .catch((err) => console.log(err));
});

app.get("/blog/create", (req, res) => {
  // res.sendFile('./view-engine/about.html',{root : __dirname});
  res.render("create", { title: "New blog" });
});



```

</br>

- add ID to some database in index.ejs :

Code :

```html

    <% if (blogs.length > 0) { %>
      <% blogs.forEach(blog => { %>
        <a class="single" href="/blogs/<%= blog._id %>">
          <h3 class="title"><%= blog.title %></h3>
          <p class="snippet"><%= blog.snippet %></p>
        </a>
      <% }) %>
    <% } else { %>
      <p>There are no blogs to display...</p>
    <% } %>


```

</br>


- add detail.ejs , to view each the blog :

Code :

```html

<html lang="en">
<%- include("../partials/head.ejs") %>

<body>
  <%- include("../partials/nav.ejs") %>

  <div class="details content">
    <h2><%= blog.title %></h2>
    <div class="content">
      <p><%= blog.body %></p>
    </div>
    <a class="delete" data-doc="<%= blog._id %>">
      <img src="/delete.svg" alt="delete icon">
    </a>
  </div>

  <%- include("../partials/footer.ejs") %>

  <script>
    const trashcan = document.querySelector('a.delete');
    trashcan.addEventListener('click', (e) => {
      const endpoint = `/blogs/${trashcan.dataset.doc}`;
      fetch(endpoint, {
        method: 'DELETE',
      })
      .then(response => response.json())
      .then(data => window.location.href = data.redirect)
      .catch(err => console.log(err));
    });
    
  </script>
</body>
</html> 


```

***

</br>

**10- Express Router & MVC:**

- We create a new folder (Routes).

- Move all the blogs path from app.js to new file in routes.(blogRoutes.js)

- instead of **app** we rename it to router.

Code -blogRoutes.js-:

```javascript

const express = require('express');

const router = express.Router();


```

- in app.js : 

```javascript

// app.use(blogRoutes);
// instead of the above code, we can add the path to this section(blog) and in the (blogRoutes) we edit the path to ('/') instead of ('/blog), ('/:id') instead of ('/blog/:id') 

// routes
app.get('/', (req, res) => {
  res.redirect('/blogs');
});

app.use('/blogs', blogRoutes);


```

***

</br>

- MVC : **M**odels, **V**iew & **C**ontroller ; 

> Controller :: controller;  
>>    Models :: Input; 
>>>     View :: Output;

*Basics:* 

> Stands for Model, View, Controller.

> MVC is a way of structuring our code & files.

> Keeps code more modular, reusable & easier to read.


<img src="./MVC.png" alt="mvc-icon" style="max-width:700px; max-height: 400px;">


</br>

So we add Controller folder, in this folder we create new directory named : **blogController.js**

```javascript

const Blog = require('../models/blog');

const blog_index = (req, res) => {
  Blog.find().sort({ createdAt: -1 })
    .then(result => {
      res.render('index', { blogs: result, title: 'All blogs' });
    })
    .catch(err => {
      console.log(err);
    });
}

const blog_details = (req, res) => {
  const id = req.params.id;
  Blog.findById(id)
    .then(result => {
      res.render('details', { blog: result, title: 'Blog Details' });
    })
    .catch(err => {
      console.log(err);
    });
}

const blog_create_get = (req, res) => {
  res.render('create', { title: 'Create a new blog' });
}

const blog_create_post = (req, res) => {
  const blog = new Blog(req.body);
  blog.save()
    .then(result => {
      res.redirect('/blogs');
    })
    .catch(err => {
      console.log(err);
    });
}

const blog_delete = (req, res) => {
  const id = req.params.id;
  Blog.findByIdAndDelete(id)
    .then(result => {
      res.json({ redirect: '/blogs' });
    })
    .catch(err => {
      console.log(err);
    });
}

module.exports = {
  blog_index, 
  blog_details, 
  blog_create_get, 
  blog_create_post, 
  blog_delete
}


```

***

</br>


- the new code of blogRoutes.js : 

Code :

```javascript

const express = require('express');
const blogController = require('../controllers/blogController');

const router = express.Router();

router.get('/create', blogController.blog_create_get);
router.get('/', blogController.blog_index);
router.post('/', blogController.blog_create_post);
router.get('/:id', blogController.blog_details);
router.delete('/:id', blogController.blog_delete);

module.exports = router;

```

***

</br>

- 


***
***

</br>
</br>
