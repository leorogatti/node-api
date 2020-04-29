# Node-api project.

## For this project you need:

* NodeJS
* Nodemon
* MongoDB

# NodeJS
![](https://user-images.githubusercontent.com/57969961/80528023-a4f13a80-896b-11ea-80ab-3a23de16f33a.jpg)
## What is Node?

* **Node.js** is a *JavaScript* interpreter that signs with open source, event-driven, created by *Ryan Dahl in 2009*, focused on migrating a *JavaScript* programming from the client **(front-end)** to servers, creating highly scalable applications (such as a server web), handling thousands of simultaneous connections / events in real time on a single physical machine.

## How can i install the Node?

* First you must enter in the [Node](https://nodejs.org/en/download/) site
![](https://user-images.githubusercontent.com/57969961/80529951-ac661300-896e-11ea-8e99-bc2f3f846c6d.png)
>And select your operational system: [Windows](https://www.microsoft.com/pt-br/windows/), [macOs](https://www.apple.com/br/macos/what-is) or [Linux](https://ubuntu.com/download/desktop).

***Or you can install with a package installer.***

# In the project.

>First i verified if **Node** and **npm** has been installed:
 ```ch
 node -v
 ```
 ```ch
  npm -v
 ``` 
 >(npm becomes with NodeJS)
#### So i started creating the **structure** in the terminal.

```ch
  mkdir node-api
```
```ch
  code node-api
```
```ch
  cd node-api 
```
```ch
  npm init -y
```
```ch
  npm install express
```

#### Later i created the first route.
```ch 
node server.js
```
```ch
http://localhost:3001/
```
>And i tested for verify if is working

```JavaScript
const express = require('express');

const app = express();
app.get("/", (req, res) => {
    res.send("Hello World");
});

app.listen(3001);
```
####  And then I installed the nodemon.
```ch
npm install -D nodemon
```
>Then i canceled the node server.js and apply:
```ch
npm run dev
```
#### Installing MongoDB 

First, we need the [Docker](https://www.docker.com/get-started)

**After the Docker installation we write this in terminal:**
```ch
docker pull mongo
```
```ch
docker run --name mongodbrs -p 27017:27017 -d mongo
```
```ch
docker ps
```
```ch
http://localhost:27017/
```

#### Then i connect the Database

```ch
npm install moongose 
```
code in server.js:
```JavaScript
const mongoose = require('mongoose');
mongoose.connect(
    'mongodb://localhost:27017/nodeapi',
    { useNewUrlParser: true }
);
```

#### Creating model of product

require-dir library:
```ch
require('./src/models/Product');
```
```ch
npm install require-dir
```

#### Restructuring of the products

organization, creation, update, deletion and listing of each product.
```ch
/src/routes.js
```
```ch
http://localhost:3001/api
```
```ch
/src/controllers/ProductController.js
```
```ch
http://localhost:3001/api/products
```
#### Using insomnia

**First i added this in ProductController.js:**
```JavaScript
const mongoose = require('mongoose');

const Product = mongoose.model('Product'); 

module.exports = {
  async index(req, res) {
    const { page = 1 } = req.query;
    const products = await Product.paginate({}, { page, limit: 10});

    return res.json(products);
  },

  async show(req, res) {
    const product = await Product.findById(req.params.id);

    return res.json(product);
  },

  async store(req, res) {
    const product = await Product.create(req.body);

    return res.json(product);
  },

  async update(req, res) {
    const product = await Product.findByIdAndUpdate(req.params.id, req.body, { new: true })

    return res.json(product);
  },

  async destroy(req, res) {
    await Product.findByIdAndRemove(req.params.id)

    return res.json();
  }
};
```

**Second i added this in routes.js:**
```JavaScript
const routes = express.Router();

const ProductController = require('./controllers/ProductController');

routes.get('/products', ProductController.index);  
routes.get('/products/:id', ProductController.show);
routes.post('/products', ProductController.store);
routes.put('/products/:id', ProductController.update);
routes.delete('/products/:id', ProductController.destroy);

module.exports = routes;
```

## Result
![](https://user-images.githubusercontent.com/57969961/80552088-f44f5f00-899b-11ea-8223-24542be535ad.png)

#### And i used the Robo3T for check the database

![](https://user-images.githubusercontent.com/57969961/80552510-3fb63d00-899d-11ea-92ff-40d89562b786.png)

# *Thanks for read.



