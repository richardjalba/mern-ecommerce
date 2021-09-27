# mern-ecommerce

This ecommerce web app demonstrates my ability using the MERN stack.

Here is where I will document my efforts in building this ecommerce app.

First I create the Header and Footer components to bring into the App. I'll also be using bootswatch for a free bootstrap theme.

**react-bootstrap**
This allows you to utilize a UI library so you can import bootstrap features directly as React components. Instead of having to use a div with a bootstrap class.

Now I'm able to use bootstrap for formatting and to bring in Navbar, Nav, Container, Button, etc.

**font-awesome**
This gets me access to a variety of icons via classNames.
https://cdnjs.com/libraries/font-awesome

Now I'm bringing in some dummy product data to work on the product listing appearance on the frontend. After I get that figured out, I'll get rid of the dummy data to build out an actual backend.

To build out the frontend, I'm creating a HomeScreen where for each product will be a listing. Each listing is a Product component made of a bootstrap Card that contains a hyperlink, image, product title, rating, and price.

The ratings will be built into a Rating component that utilizes font-awesome icons. Then I manipulate Rating component propTypes so the inputs are strictly strings, numbers, etc. and so some of these properties are required.

**react-router-dom** & **react-router-bootstrap**
This enables dynamic routing within a web application. In this specific case, we are integrating it with bootstrap.

I import BrowserRouter under the alias of Router. This allows me to access HTML history api, so I can use history.pushState() and history.replaceState().

Then I wrap everything in App with the Router. This lets me bring in the Route tags so I can select paths and their resulting componentScreen. I make sure to put the 'exact' attribute for the HomeScreen.

I create the ProductScreen to back and forth with the HomeScreen via routing. The paths for products includes :id since these will be unique.

I switch out the 'a' tags for LinkContainer tags in the Navbar. And I switch out the 'a' tags in the Product components for Link tags.

Note: LinkContainer is used for bootstrap components.

By using the Link and LinkContainer tags, we're skipping the reloads you'd typically experience with 'a' tags.

Now I'm building out the ProductScreen. Where I run into two issues:

1. I keep getting an error instead of a product page on the client side. The solution is to import BrowserRouter from react-router-dom.

2. My bootstrap skills need work. I'm much more used to CSS/SCSS. I figure out to add attribute 'fluid' to prevent the image from spilling out of its container.

Put in some logic that determines whether the Add to Cart button is enabled or disabled.

Here is where I introduce the backend using Node, express, and MongoDB. Using Node, I can communicate the backend server with the database.

**Express** will be used to create routes in the backend, which holds JSON data that can be served to the frontend.

This JSON data is accessed by using an HTTP request from the frontend, aka GET, PUT, POST, DELETE, to interact with the backend express framework.

These HTTP methods are what keep things RESTful. An "architecture" or style that keeps things practical and efficent for fetching, adding, updating, and deleting.

I create a backend folder in the root, where I create server.js to use as an entrypoint for the server. I also create a folder to put in a copy of the dummy data. I'm putting in a copy and not deleting the original dummy data to avoid frontend errors.

I build out server.js to have a home route and api/products(/:id) routes. I modify scripts in the root package.json so I can run the backend server with npm start.

I run into an issue where the dummy backend data doesn't want to be fetched, when using the URL http://localhost:5000/api/products

The solution is that the syntax in the backend is in Vanilla JS. Which I'll change in a bit. After I use the module.exports syntax, I'm able to fetch the dummy backend data.

Back in the frontend I want to pull the JSON data from the backend dummy data straight into the frontend display for the user to see.

**axios** is an HTTP library that allows us to make HTTP requests to the backend.

In the front end, I bring the useState hook from react into the HomeScreen. Where I call the state [products, ] and the function to change the state [ , setProducts]. The default state is passed through useState([]), which is an empty array in this case.

(Things like products and users are usually part of the global state via redux. But for now, products will be on a component level, as of now.)

Then I bring in the UseEffect hook to make a request to the backend. Anything put in useEffect will run as soon as the component loads.

I use Async/Await to make the fetch request within the UseEffect. You might want to look at the code and see how this is done, since my brain sort of stumbled into this, since I didn't want to use .then syntax. This way setProduct can get the data from the backend route directly.

The second argument to useEffect is empty since there are no dependencies (something that triggers when the given variable changes).

After I set up a proxy, I'm able to see the frontend fetch the HomeScreen product listings from the backend. I need to use the proxy because the routes are set to port 5000 and the frontend is set to 3000. Changing this on the server.js leads to a CORS error, or "domain" error.

Then I get the ProductScreen hooked up with useState and useEffect, and bring in axios. But not without removing the imports that connect it to the dummy data first. Since the ProductScreens are still pulling from the original dummy data I have placed in the frontend since the beginning.

The code for the hooks in ProductScreen are the same as HomeScreen. Except instead of products, it is product, and the get request is changed to include the id that's given in the URL.

Once that works, I delete the original dummy data in the frontend. Leaving the dummy data in the backend folder. Which will be removed after a database is implemented.

**nodemon** and **concurrently** are used for development so I don't have to repeatedly restart my server for any code changes I make AND so I can have both frontend and backend run at the same time. I change the scripts in the JSON file to best utilize these tools.

**dotenv** allows us to set up environment variables. I change a few things is server.js to connect to my .env file.

Now I want to change the Vanilla JS syntax to ES import syntax. I do this by adding "type": "module" to my package.json.

This leads to an error in the products.js dummy data, which is fixed by changing the export syntax.
