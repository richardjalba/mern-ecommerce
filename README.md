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
