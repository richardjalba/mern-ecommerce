# mern-ecommerce

This ecommerce web app demonstrates my ability using the MERN stack.

EMAIL: admin@example.com
PASSWORD: 123456

PAYPAL
EMAIL: sb-43mghc8052923@personal.example.com
PASSWORD: N[8wM0u$

**Here is where I will document my efforts in building this ecommerce app.**

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

**MongoDB** is a NoSQL database that utilizes JSON. Every "document" is given automatically given an \_id property.

MongoDB will let us create a collection for users, orders, and products.

I get my cluster set up and put the URI and other pertinent info in the .env file.

**mongoose** allows us to create models and schema in our MongoDb database. Object modeling.

In the backend folder, I create the config folder to hold the db.js file. Which contains an asynchronous function since dealing with MongoDB via .connect, .find, .create, will return promises.

Then I bring this in server.js as connectDB. Initially, I ran into an issue because I forget the .js since the backend folder is using node.

**colors** is used on the developer side to make things easier to see in the console. I'm using this package so it's easier for me to see whether my connection to mongo is working or not.

I create a models folder for orderModel, productModel, and userModel. Within each file, I use mongoose to create schemas as objects that contain all the fields per model.

I also throw in the Review schema within the productModel.js file since it seemed appropriate.

Now I modify the dummy products data and get rid of the \_id field since I want to see MongoDB add that automatically when I send it the data.

I also create some dummy user data, where I create an admin user and I need to hash the passwords.

**bcryptjs** is used to hash passwords for added security.

At this point, I got frustrated that my products were no longer appearing on their ProductScreen. Eventually I realize this is because I removed the \_id fields in the dummy data.

I create a standalone seeder.js file that takes in mongoose and env. It also takes in the Models files and dummy data files.

This seeder.js file will clear data that's already in the database, then it will insert the data I have in the products.js and users.js files, which are dummy data. The Admin user is assigned to the inserted products.

I also put in a function to simply destroy all data in case I'm feeling cheeky.

I give both the import and destroy functions their own scripts in the package.json file.

I repeatedly use the destroy and import scripts when my Mongo Compass app doesn't pick up the data I supposedly seeded. Turns out I needed to click Reload Data in the Compass app. So everything was actually working fine.

I create the routes folder with productRoutes.js inside of it. Then I move the product routes from the server.js file to the productRoutes.js file.

After tweaking server.js, I bring in the Product model into productRoutes.js and build out the file.

**express-async-handler** is a middleware that handles exceptions inside async express routes and passes them to your express error handlers.

This package is applied by wrapping the route async function with the alias given, asyncHandler.

I jump onto my Postman app to play around with my APIs to see that everything is working.

Since I don't want the default error handler when the URL :id isn't recognized, since it's HTML, I create a custom middleware error handler that serves JSON instead of the default HTML.

In errorMiddleware.js, to overwrite the default error handler, I need to use the following syntax (err, req, res, next). The 'next' is always needed for middleware, but the 'err' is specific to overriding the default error handler.

I go back to Postman to play with GETting an invalid :id to see if my middleware is working. It is, after I import my middleware fx's to server.js.

I do the same with invalid routes (ex. /api/chickenteriyaki) so a Not Found error is served.

At this point, the backend and frontend are communicating properly. The main issue is that this is on a component-level.

Now I need to bring in redux so I can bring things like products, users, and orders on a global level.

Here is the best YouTube video I can find that describes how Redux works: https://www.youtube.com/watch?v=np8A_aW7Pew

(That video is more for my own reference.)

**redux** is state manager.

**react-redux** gets redux to work with react.

**redux-thunk** lets us make async requests within action creators; middleware.

**redux-devtools-extension** lets me use the chrometool to observe redux state management.

I create the store.js file and put each of these packages into use to connect my Reducers and related middleware.

In index.js, I import store.js and Provider from redux.

Then I create productListReducer in the productReducers, so I have a case for REQUEST, SUCCESS, FAILURE.

I also create a constants folder with a productConstants file, which I build out and bring into productReducers.js.

Then I create an actions folder with productActions.js. Where I bring in the productConstants.

Do you remember how we hav useEffect to fetch the products data in the HomeScreen component? Now we're gonna move that functionality into the productActions.js file.

I do this by bringing in axios, using a "double arrow" syntax for thunk, and dispatching the REQUEST Constant which is already tied to trigger its given Reducer, followed by an axios request, followed by dispatching SUCCESS, which serves a payload that gets passed down to the state.

If something goes wrong, we instead dispatch FAILURE to serve the payload with an error message.

Back in HomeScreen.js we can remove the component state, since we're moving our resources (products, users, orders) to global data via redux.

This means we're clearing the useEffect and utilizing the productList action inside it instead, after bringing in the action file into HomeScreen.

We're also bringing in the useDispatch and useSelector functions from react-redux. Which we'll use hooks to bring in useDispatch for use in useEffect, and useSelector for us to select the state we want.

To break things up and at some flavor, I create a Loader and Message component. So whenever the state is loading during a fetch request, we'll get a bootstrap animation until the request is a success, or a message if the request fails.

Now that we've got the products on a global level, we need to move the product descriptions from the component-level to the global level too.

This is essentially a repeat of what I've already written, albeit singular items and into the ProductScreen component: 1) Make constants for product details. 2) Make product details reducer. 3) Add the reducer to store.js. 4) Make listProductDetails action 5) bring all these into the ProductScreen

Now I want to add quantity to the ProductScreen, so I set the state for quantity. Then I set a ListGroup.Item to appear if the stock is more than 0.

Then I give the Add to Cart button an onClick addToCartHandler. Which adds to cart the quantity selected on the ProductScreen. While also taking the user to the CartScreen.

Then I build out the CartScreen and bring the route into App.js.

Now I work on Cart functionality by building out the respective Constant, Reducer, Action. Bring this into the store.js file.

Note: The cart is saved to local storage in JSON format. This way I can bring it into the store.js file.

To clean things up a bit, I simply move the functionality from productRoutes.js to productController.js.

Now productRoutes.js only has the routes and the functions that are imported from productController.js.

I build out the userModel (somewhat based on the productModel) and the userController.

The userController will authorize the user and collect a token.

Added express.json to serverjs. That way I can access req.body.email and req.body.password in the userController file.

In the userController file I create an authUser function to pull the email and password from the frontend and POST it to the backend.

Back in userRoutes file, I put in a route with a POST request that triggers the authUser function.

Then I mount this into the server.js file as app.use('/api/users', userRoutes).

**jsonwebtoken** is made of a header, payload, and signature verification. All this can tell whether the user is who they say they are and can authorize for any private routes.

I create a utils folder with a generateToken.js file. I import the jsonwebtoken passage and create the generateToken function that takes in an id as the payload for the token. So I sign(id), followed by the secret, which I put in my .env, then follow the secret with an expiration of 30 days.

Back in the userController, every time a user logs in (which is a POST request), the backend will send back the users information along with a generated webtoken that contains the user's \_id as the payload.

Now I'm creating middleware to use the token to access protected routes; user profile, orderhistory, etc. I import jwt and userModel. The function is called protect.

In the userController, I create a GET request function to get the user's profile (a private route). And I also bring this into the userRoute file, where I include the protect middleware function in the profile get request.

In userController, I build out a function to register a new user. Then I import this into userRoutes and add the POST request route to the home route '/'.

Now, back in the front-end.

I start off my creating a userConstants file for logout and login requests, success, and failure. Then I create the userReducers file where I build out userLoginReducer; which I bring into store.js.

Then I create the userActions file that I build out the login function for.

Login takes in an email and password. Then it can dispatch USER_LOGIN_REQUEST along with config, which attaches a token to the header. Then it will post onto the login api, along with the given email, password, and the config. Then USER_LOGIN_SUCCESS while saving the data to local storage.

The catch errors will all pretty much be the same across the app.

Back in store.js I create userInfoFromStorage to pull the users data from the local storage. And add userLogin to initialState.

Now I create the LoginScreen and FormContainer components. After I build those out, I add the route to the LoginScreen in the App.js file.

I modify the Header so if the localStorage has the userInfo, the Sign In text will change to the user's name and a dropdown will give the user access to their profile and a logout link.

Then I create a logout action in userActions.

...

I create userRegisterReducer in userReducers. Then I add it to the store.js file. Next I add register to userActions. This is very similar to login.

Aftwerwards I build out the RegisterScreen. Which is similar to LoginScreen. Except there are more redux useState hooks and (now including name, confirmPassword, message). Along with a few other changes in the form and message.

Now I want to get the backend setup so I can create a ProfileScreen in the frontend.

So I'll start at the userController and create a POST to updateUserProfile (name, email, password).

Then inside the userRoutes file, I add a .put to the/profile route.

Afterwards I go on postman to make sure these API's are working properly. I couldn't get it to work at first because I forgot about my protect middleware. Everything is working fine.

I go to userConstants and userReducers for USER\__DETAILS_-----. Then I add the reducer to the store.js file. Next I add getUserDetails to userActions.

In the Screens folder I create the ProfileScreen file to build out. Much of the logic is based on the ProfileScreen, but with some changes. The JSX is similar except with profile info on the left and orders on the right side of the screen.

Then in app.js I add a route for the profileScreen. And I add the user update constants in the userConstants file, followed by adding userUpdateProfileReducer to userReducers.js and updateUserProfile to userActions.

As of now, if I'm in the checkout process and I click next for shipping, I get taken to the loginScreen which you can see has a redirect to shipping in the redirect on sign-in.

To start off, I create the ShippingScreen and give it a route in App.js. In cartActions I create saveShippingAddress along with it's partnering reducer in cartReducers.

In store.js I create the function shippingAddressFromStorage since this data will need to be stored in the localStorage.

Then I modify the code in shippingScreen to pull out shipping address data in the local storage to fill in the appropriate fields.

Now I created CheckoutSteps component for breadcrumbs through the purchase process. Which I bring into the shippingScreen and into App.js as a route.

Next I create and build out the PaymentScreen. Where I use paymentMethod for setState. In the cartConstants, I put in CART_SAVE_PAYMENT_METHOD. Which is brought into cartActions as a function savePaymentMethod; and also saves data to localStorage.

Now I create and build out the PlaceOrderScreen, which takes in the cart state. In the backend, I make an orderController that uses a POST request, as well as orderRoutes.

Back in the frontend, we want to be able to place an order. So I create orderConstants, orderReducers, and orderActions. Then I modify the PlaceOrderScreen.

Now I'm going to work on the OrderScreen, but first I need to fetch the order from the database. So in OrderController, I create a GET request with an :id via private route. I try the route out on Postman to see if it's working properly - it is.

Now we want to get the order details and bring them into the OrderScreen. So I start by adding the \_DETAILS\_ to the orderConstants. Then I make the orderDetailsReducer in the orderReducers file; which is then added to store.js. Next in the orderActions I create getOrderDetails.

Now we're able to fetch the order and send it through the state, I'll build out the OrderScreen. I used the PlaceOrderScreen as the template and modify it as necessary. Which I then import and make a route for in App.js.

Before bringing in PayPal and using their api, I need to make sure I can get an order to update to being paid in the database.

In the orderController, I add updateOrderToPaid. Then in orderRoutes, I add a route for a PUT request. Then in the frontend, I fix up the order pay CONSTANTS, Action, and Reducer. Which I bring into store.js.

I get the api I need from paypal's website and insert it into my env file. Then I add the GET route in my server.js file.

In the OrderScreen, I bring in axios and a PayPal sdk script. The sdk script is utilized within a useEffect.

**react-paypal-button-v2** is imported into the OrderScreen and shows in the frontend when the order is not paid. This takes in the amount to be paid and takes in a success handler.

I create successPaymentHandler in the OrderScreen file... I test out the order payment processing via the dummy accounts paypal provides. Success.

Now I want to show the orders on the ProfileScreen. So first I need to go to the orderController to add a GET route to access the orders to the user that is logged in. The route is added to orderRoutes. I test it in Postman - Success.

Then I add this to the Constants, Reducer, Action, bring the action in the ProfileScreen, which I build out even more to show the order information, and call it to bring it onto the state.

Now I'm gonna focus on admin functionality.

In userController, I add a GET request to get all users (getUsers) via private AND admin access. Then I add the route to userRoute. Followed by adding admin to my authMiddleware.

In the userConstant file, add USER\_\_LIST. Add userListReducer to userReducers. In userActions add listUsers.

Now I'm creating UserListScreen where I bring in everything mentioned in the last two paragraphs. Then I add UserListScreen to App.js.

...

Now I'm going to create the delete user functionality. So in userController I make a DELETE api via a private admin route. Then I bring it into the userRoutes and userConstants.

Then create a userDeleteReducer in the userReducers. Followed by adding it to store.js, then adding deleteUser in userActions.

Then this functionality is added to the UserListScreen.

Now I want to GET a user to show on screen and UPDATE. So I create getUserById in the userController. And I create updateUser as a PUT api - this allows change to whether a person is admin. Then I add this put in the userRoutes.

Now I'm creating the UserEditScreen. Based on the RegisterScreen, except with the appropriate logic.

I make a userUpdate constant, reducer, etc, to get the UserEditScreen to actually function.

.....

Now I want to manage products and create ProductListScreen. Based on UserListScreen with appropriate modifications. Then I add this to App.js

Next I want to add the product delete functionality. So I start at the productController to add  deleteProduct and add that to productRoutes. I test out the DELETE api on Postman and it works. Followed by making the changes to the productConstants, productReducers, and productActions.

Repeat the previous passage for create product POST and update product PUT functionality.

I modify the ProductListScreen to include the create, delete, and modify buttons and handlers. 

Next I create the ProductEditScreen. Based on the UserEditScreen with appropriate modifications.

These product routes get added to App.js.

**Multer** is used for uploading files. 

The documentation was confusing and the syntax was kinda weird. But I'm implementing it for product functionality.

NOTE: The image must be JPG, JPEG or PNG.

All files are uploaded to a folder called uploads. The route is put into updateRoutes.js. 

The server.js file and ProductEditScreen are modified.

.....


**Morgan** is a logger that helps create an endpoint to log to review product.

Morgan is passed in as middleware, which is utilized in the server.js file.

createNewReview is added to productController.js and given all typical redux code in their appropriate file locations.

The review functionality and form is added to the ProductScreen state.

.....

SearchBar component is created and added to the Header via react-router-dom render props so we can have access to the history. The search route is added to App.js.

productController is getProducts to fetch the products that match the keyword in the SearchBar.

.....

For the carousel on the top of the page. Modify the productController to GET top rated products. 

Top Review Product given all typical redux code in their appropriate file locations.

ProductCarousel component created.

.......

FIN
