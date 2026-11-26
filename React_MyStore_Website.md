# React Project: MyStore Website

## 1. Project goal

In this practical lesson, students will build a simple four-page
shopping website using React.

The website contains:

-   **Home** -- a welcome message, short description, image and Shop Now
    link.
-   **About** -- a short introduction to the store with an image.
-   **Products** -- reusable product cards created with a React
    component and props.
-   **Contact** -- a simple contact form layout.

The main teaching goal is to understand **what each React function or
feature does, why we use it, and where it is used**.

------------------------------------------------------------------------

## 2. Requirements

Install these before starting:

-   Node.js
-   Visual Studio Code
-   A web browser

Check Node.js and npm in the VS Code terminal:

``` bash
node -v
npm -v
```

## 3. Create the React project

Run these commands in the terminal:

``` bash
npm create vite@latest react-01 -- --template react
cd react-01
npm install
npm install react-router-dom
npm run dev
```

Vite displays a local development URL, usually `http://localhost:5173`.

> If the project already exists, open its folder in VS Code and run
> `npm install` and `npm install react-router-dom` as needed.

------------------------------------------------------------------------

## 4. Project folder structure

Create the following files inside `src`:

``` text
src/
│
├── components/
│   ├── Navbar.jsx
│   └── Navbar.css
│
├── pages/
│   ├── Home.jsx
│   ├── Home.css
│   │
│   ├── About.jsx
│   ├── About.css
│   │
│   ├── Products.jsx
│   ├── Products.css
│   │
│   ├── Contact.jsx
│   └── Contact.css
│
├── App.jsx
├── App.css
└── main.jsx
```

### Why do we create folders?

-   `components/` contains reusable parts of the website. The Navbar can
    be displayed on every page.
-   `pages/` contains the main content for each route: Home, About,
    Products and Contact.
-   `App.jsx` connects the Navbar and the page routes.
-   `App.css` contains global styling shared by the application.
-   `main.jsx` is the entry point that starts the React application.

------------------------------------------------------------------------

# 5. Source Code

## File 1: `src/main.jsx`

``` jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';

import App from './App.jsx';
import './App.css';

ReactDOM.createRoot(document.getElementById('root')).render(
    <React.StrictMode>
        <BrowserRouter>
            <App />
        </BrowserRouter>
    </React.StrictMode>
);
```

### Explanation

**What is `main.jsx`?**

`main.jsx` is the starting point of this React application. It connects
the React application to the HTML page.

**React functions and features used:**

  -----------------------------------------------------------------------------------
  Name                                What it does            Why we use it
  ----------------------------------- ----------------------- -----------------------
  `ReactDOM.createRoot()`             Creates a React root    It tells React where to
                                      inside an HTML element. display the
                                                              application.

  `document.getElementById('root')`   Finds the HTML element  Vite's `index.html`
                                      whose ID is `root`.     contains this element.

  `.render()`                         Displays the React      It renders our App
                                      element tree.           component in the
                                                              browser.

  `React.StrictMode`                  Enables additional      It can help identify
                                      development checks.     common problems while
                                                              developing.

  `BrowserRouter`                     Enables browser-based   It allows the app to
                                      routing.                show different pages
                                                              for different URLs.
  -----------------------------------------------------------------------------------

**Important:** `BrowserRouter` is placed here once. Do not wrap the app
in another `BrowserRouter` inside `App.jsx`.

------------------------------------------------------------------------

## File 2: `src/App.jsx`

``` jsx
import { Routes, Route } from 'react-router-dom';

import Navbar from './components/Navbar';

import Home from './pages/Home';
import About from './pages/About';
import Products from './pages/Products';
import Contact from './pages/Contact';

function App() {
    return (
        <>
            <Navbar />

            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/about" element={<About />} />
                <Route path="/products" element={<Products />} />
                <Route path="/contact" element={<Contact />} />
            </Routes>
        </>
    );
}

export default App;
```

### Explanation

**What is `App.jsx`?**

`App.jsx` is the main application component. It brings together the
Navbar and all four page components.

**React functions and features used:**

  -----------------------------------------------------------------------
  Name                    What it does            Why we use it
  ----------------------- ----------------------- -----------------------
  `function App()`        Declares a JavaScript   We use it to define the
                          function component.     main application UI.

  `return`                Returns the JSX that    React needs the UI
                          the component displays. description from the
                                                  component.

  `Routes`                Groups route            It tells React Router
                          definitions.            which route should be
                                                  matched.

  `Route`                 Maps a URL path to a    For example, `/about`
                          component.              displays the About
                                                  component.

  `export default App`    Exports the component.  `main.jsx` imports and
                                                  displays it.

  `<>...</>`              React Fragment          It groups Navbar and
                          shorthand.              Routes without adding
                                                  an extra HTML element.
  -----------------------------------------------------------------------

**Understand the routes:**

  URL           Component displayed
  ------------- ---------------------
  `/`           Home
  `/about`      About
  `/products`   Products
  `/contact`    Contact

------------------------------------------------------------------------

## File 3: `src/components/Navbar.jsx`

``` jsx
import { Link } from 'react-router-dom';
import './Navbar.css';

function Navbar() {
    return (
        <nav className="navbar">

            <h2>MyStore</h2>

            <div className="nav-links">
                <Link to="/">Home</Link>
                <Link to="/about">About</Link>
                <Link to="/products">Products</Link>
                <Link to="/contact">Contact</Link>
            </div>

        </nav>
    );
}

export default Navbar;
```

### Explanation

**What is a component?**

A component is a reusable part of the user interface. Here, `Navbar` is
a component that displays the website navigation.

**React functions and features used:**

  -------------------------------------------------------------------------
  Name                      What it does            Why we use it
  ------------------------- ----------------------- -----------------------
  `function Navbar()`       Creates a function      It defines the
                            component.              navigation bar UI.

  `return`                  Returns the navigation  It tells React what to
                            JSX.                    display.

  `Link`                    Creates an internal     It changes routes
                            navigation link.        without a full-page
                                                    browser reload.

  `className`               Assigns a CSS class in  We use it to style the
                            JSX.                    navigation elements.

  `export default Navbar`   Exports the component.  `App.jsx` can import
                                                    and reuse it.
  -------------------------------------------------------------------------

**Why use `Link` instead of a normal `<a>` tag?**

For internal React Router navigation, use:

``` jsx
<Link to="/about">About</Link>
```

A normal anchor such as `<a href="/about">` can cause a full-page
navigation. React Router's `Link` performs client-side navigation.

------------------------------------------------------------------------

## File 4: `src/components/Navbar.css`

``` css
.navbar {
    background: #202b46;
    color: white;
    padding: 20px 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.navbar h2 {
    font-size: 26px;
}

.nav-links {
    display: flex;
    gap: 30px;
}

.nav-links a {
    color: white;
    text-decoration: none;
    font-size: 16px;
}

.nav-links a:hover {
    color: #9db8ff;
}

@media (max-width: 600px) {
    .navbar {
        flex-direction: column;
        gap: 18px;
        padding: 20px;
    }

    .nav-links {
        gap: 15px;
        flex-wrap: wrap;
        justify-content: center;
    }
}
```

### CSS explanation

-   `display: flex` places the brand and navigation links in a row.
-   `justify-content: space-between` places space between the brand and
    links.
-   `align-items: center` aligns them vertically.
-   `gap` controls spacing between links.
-   `:hover` applies a style when the mouse pointer is over a link.
-   `@media` applies different CSS rules on smaller screens.

------------------------------------------------------------------------

## File 5: `src/pages/Home.jsx`

``` jsx
import { Link } from 'react-router-dom';
import './Home.css';

function Home() {
    return (
        <div className="home-container">

            <div className="home-content">
                <h1>Welcome to MyStore</h1>

                <p>
                    Discover the latest electronics, smart gadgets
                    and accessories at affordable prices.
                    Quality products, great deals and a better
                    shopping experience.
                </p>

                <Link to="/products">
                    <button>Shop Now</button>
                </Link>
            </div>

            <div className="home-image">
                <img
                    src="https://images.unsplash.com/photo-1490481651871-ab68de25d43d?w=800"
                    alt="Shopping collection"
                />
            </div>

        </div>
    );
}

export default Home;
```

### Explanation

**What is the Home component?**

It displays the first page visitors see when they open the website.

**React functions and features used:**

  -----------------------------------------------------------------------
  Name                    What it does            Why we use it
  ----------------------- ----------------------- -----------------------
  `function Home()`       Creates the Home page   It keeps the Home page
                          component.              code separate.

  `return`                Returns the Home page   It describes the page
                          JSX.                    UI.

  `Link`                  Navigates to another    The Shop Now link opens
                          route.                  the Products page.

  `className`             Adds CSS class names.   It connects JSX
                                                  elements to Home.css.

  `export default Home`   Exports the component.  `App.jsx` can import
                                                  it.
  -----------------------------------------------------------------------

**Understand JSX expressions:**

In React, we write HTML-like elements inside JavaScript. This syntax is
called JSX.

Example:

``` jsx
<h1>Welcome to MyStore</h1>
```

`className` is used instead of HTML's `class` attribute in JSX.

------------------------------------------------------------------------

## File 6: `src/pages/Home.css`

``` css
.home-container {
    display: flex;
    align-items: center;
    justify-content: space-around;
    padding: 60px;
    gap: 40px;
    background: white;
    min-height: 450px;
}

.home-content {
    width: 45%;
}

.home-content h1 {
    font-size: 42px;
    color: #202b46;
    margin-bottom: 20px;
}

.home-content p {
    font-size: 17px;
    line-height: 1.8;
    color: #666;
    margin-bottom: 25px;
}

.home-content button {
    background: #202b46;
    color: white;
    padding: 12px 30px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.home-image {
    width: 45%;
}

.home-image img {
    width: 100%;
    height: 350px;
    object-fit: cover;
    border-radius: 12px;
}

@media (max-width: 768px) {
    .home-container {
        flex-direction: column;
        padding: 30px 20px;
    }

    .home-content,
    .home-image {
        width: 100%;
    }

    .home-content h1 {
        font-size: 30px;
    }
}
```

### CSS explanation

-   `display: flex` places the text and image side by side.
-   `width: 45%` gives each section a width of 45%.
-   `object-fit: cover` fills the image area without distorting the
    image.
-   `border-radius` rounds the image corners.
-   The media query changes the layout to a vertical arrangement on
    smaller screens.

------------------------------------------------------------------------

## File 7: `src/pages/About.jsx`

``` jsx
import './About.css';

function About() {
    return (
        <div className="about-container">

            <div className="about-content">

                <h1>About MyStore</h1>

                <p>
                    Welcome to MyStore! We are an online shopping
                    destination offering quality electronics,
                    smart gadgets and accessories at affordable prices.
                </p>

                <p>
                    Our mission is to provide customers with
                    quality products, excellent service and
                    a convenient shopping experience.
                </p>

            </div>

            <div className="about-image">

                <img
                    src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=800"
                    alt="Our store"
                />

            </div>

        </div>
    );
}

export default About;
```

### Explanation

-   `function About()` creates the About page component.
-   `return` provides the JSX to display.
-   `<div>` groups related content.
-   `<h1>` displays the page heading.
-   `<p>` displays paragraphs.
-   `<img>` displays an image.
-   `alt` provides alternative text describing the image.
-   `className` connects the elements to About.css.
-   `export default About` makes the component available to App.jsx.

**Teaching point:** The About page uses the same component structure as
Home, but it has its own content and CSS.

------------------------------------------------------------------------

## File 8: `src/pages/About.css`

``` css
.about-container {
    display: flex;
    align-items: center;
    justify-content: space-around;
    gap: 40px;
    padding: 60px;
    background: white;
    min-height: 450px;
}

.about-content {
    width: 45%;
}

.about-content h1 {
    font-size: 38px;
    color: #202b46;
    margin-bottom: 20px;
}

.about-content p {
    font-size: 16px;
    color: #666;
    line-height: 1.8;
    margin-bottom: 15px;
}

.about-image {
    width: 45%;
}

.about-image img {
    width: 100%;
    height: 320px;
    object-fit: cover;
    border-radius: 12px;
}

@media (max-width: 768px) {
    .about-container {
        flex-direction: column;
        padding: 30px 20px;
    }

    .about-content,
    .about-image {
        width: 100%;
    }
}
```

### CSS explanation

-   Flexbox places the About text and image side by side.
-   `width` controls the space used by each section.
-   `line-height` improves paragraph readability.
-   The media query stacks the content on smaller screens.

------------------------------------------------------------------------

## File 9: `src/pages/Products.jsx`

``` jsx
import './Products.css';

function ProductCard(props) {
    return (
        <div className="card">

            <img src={props.image} alt={props.name} />

            <h2>{props.name}</h2>

            <p>{props.description}</p>

            <h3>₹{props.price}</h3>

        </div>
    );
}

function Products() {
    return (
        <div className="products-container">

            <h1>Our Products</h1>

            <ProductCard
                name="Wireless Headphones"
                image="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=500"
                description="High-quality wireless headphones."
                price="1499"
            />

            <ProductCard
                name="Smart Watch"
                image="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=500"
                description="Stylish smart watch."
                price="2499"
            />

            <ProductCard
                name="Camera"
                image="https://images.unsplash.com/photo-1516035069371-29a1b244cc32?w=500"
                description="Professional digital camera."
                price="4999"
            />

            <ProductCard
                name="Laptop"
                image="https://images.unsplash.com/photo-1496181133206-80ce9b88a853?w=500"
                description="High-performance laptop."
                price="45999"
            />

            <ProductCard
                name="Headphones"
                image="https://images.unsplash.com/photo-1484704849700-f032a568e944?w=500"
                description="Premium audio experience."
                price="1999"
            />

        </div>
    );
}

export default Products;
```

### Explanation

This is the most important page for teaching **React components and
props**.

There are two function components in this file:

#### A. `ProductCard(props)`

``` jsx
function ProductCard(props) {
    return (
        <div className="card">
            <h2>{props.name}</h2>
            <p>{props.description}</p>
            <h3>₹{props.price}</h3>
        </div>
    );
}
```

-   `ProductCard` is a reusable component.
-   `props` is the object that receives values passed by the parent
    component.
-   `props.name` reads the product name.
-   `props.description` reads the product description.
-   `props.price` reads the product price.
-   `props.image` reads the image URL.

#### B. `Products()`

This is the parent component. It calls `ProductCard` five times and
passes different values each time.

Example:

``` jsx
<ProductCard
    name="Laptop"
    image="laptop-image-url"
    description="High-performance laptop."
    price="45999"
/>
```

The values passed here are called **props**.

### Why use a reusable component?

Without a reusable component, we would write the same card HTML
repeatedly.

With `ProductCard`, we write the card design once and reuse it with
different product information.

**Important:** Props are passed from parent to child. In this example,
`Products` is the parent and `ProductCard` is the child.

------------------------------------------------------------------------

## File 10: `src/pages/Products.css`

``` css
.products-container {
    padding: 40px;
    text-align: center;
}

.products-container h1 {
    color: #202b46;
    margin-bottom: 30px;
}

.card {
    display: inline-block;
    width: 230px;
    margin: 15px;
    padding: 15px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 2px 10px #ddd;
    vertical-align: top;
}

.card img {
    width: 100%;
    height: 160px;
    object-fit: cover;
    border-radius: 8px;
}

.card h2 {
    font-size: 20px;
    margin: 15px 0;
}

.card p {
    color: #666;
    margin-bottom: 12px;
}

.card h3 {
    color: #202b46;
}
```

### CSS explanation

-   `display: inline-block` allows cards to sit next to each other and
    wrap onto another line when needed.
-   `width` sets the card width.
-   `margin` creates space around each card.
-   `padding` creates space inside each card.
-   `box-shadow` adds a shadow.
-   `object-fit: cover` keeps product images filling their image area.

------------------------------------------------------------------------

## File 11: `src/pages/Contact.jsx`

``` jsx
import './Contact.css';

function Contact() {
    return (
        <div className="contact-container">

            <h1>Contact Us</h1>

            <p>
                Have questions? We would love to hear from you.
            </p>

            <form className="contact-form">

                <input
                    type="text"
                    placeholder="Enter Your Name"
                />

                <input
                    type="email"
                    placeholder="Enter Your Email"
                />

                <input
                    type="text"
                    placeholder="Enter Subject"
                />

                <textarea
                    placeholder="Enter Your Message"
                ></textarea>

                <button type="button">
                    Send Message
                </button>

            </form>

        </div>
    );
}

export default Contact;
```

### Explanation

-   `function Contact()` creates the Contact page component.
-   `return` returns the page JSX.
-   `<form>` groups the form controls.
-   `<input>` accepts short user input.
-   `type="text"` is used for ordinary text.
-   `type="email"` is used for email input.
-   `placeholder` displays hint text inside an empty field.
-   `<textarea>` accepts a longer message.
-   `button` displays the Send Message control.
-   `type="button"` means this button does not submit the form
    automatically.

**Important:** This is only a front-end form. It does not send messages
to an email address or save them to a database. Form handling can be
taught in a later lesson.

------------------------------------------------------------------------

## File 12: `src/pages/Contact.css`

``` css
.contact-container {
    background: white;
    padding: 60px 20px;
    text-align: center;
    min-height: 450px;
}

.contact-container h1 {
    font-size: 36px;
    color: #202b46;
    margin-bottom: 15px;
}

.contact-container p {
    color: #666;
    margin-bottom: 30px;
    font-size: 16px;
}

.contact-form {
    max-width: 450px;
    margin: auto;
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.contact-form input,
.contact-form textarea {
    width: 100%;
    padding: 14px;
    border: 1px solid #ccc;
    border-radius: 6px;
    font-size: 15px;
    outline: none;
}

.contact-form input:focus,
.contact-form textarea:focus {
    border-color: #202b46;
}

.contact-form textarea {
    height: 120px;
    resize: vertical;
}

.contact-form button {
    background: #202b46;
    color: white;
    padding: 14px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 16px;
}

.contact-form button:hover {
    background: #405783;
}

@media (max-width: 600px) {
    .contact-container {
        padding: 35px 20px;
    }
}
```

### CSS explanation

-   `max-width` limits the form width.
-   `margin: auto` horizontally centers the form when space is
    available.
-   `flex-direction: column` places the form fields vertically.
-   `gap` creates space between fields.
-   `:focus` changes the border when a user selects an input.
-   `resize: vertical` allows the user to change the textarea height
    vertically.

------------------------------------------------------------------------

## File 13: `src/App.css`

``` css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #f4f6f9;
    color: #333;
}
```

### Explanation

`App.css` contains global styles that apply across the website.

  -----------------------------------------------------------------------
  CSS                                 Purpose
  ----------------------------------- -----------------------------------
  `*`                                 Selects all elements.

  `margin: 0`                         Removes default outside spacing.

  `padding: 0`                        Removes default inside spacing.

  `box-sizing: border-box`            Includes padding and border within
                                      the declared width and height.

  `body`                              Styles the main HTML body.

  `font-family`                       Sets the website font.

  `background`                        Sets the page background colour.
  -----------------------------------------------------------------------

Each page has its own CSS file, so page-specific styles should stay in
that page's CSS file.

------------------------------------------------------------------------

# 6. How the complete application works

Understand the flow before explaining the code to students:

``` text
index.html
    |
    v
main.jsx
    |
    |-- BrowserRouter
    |
    v
App.jsx
    |
    |-- Navbar
    |
    |-- Routes
          |
          |-- /          --> Home.jsx
          |
          |-- /about     --> About.jsx
          |
          |-- /products  --> Products.jsx
          |
          |-- /contact   --> Contact.jsx
```

The Navbar is displayed on every route. React Router changes the page
component according to the URL.

------------------------------------------------------------------------

# 7. Important React concepts covered

  -----------------------------------------------------------------------
  Concept                 Meaning                 Used in
  ----------------------- ----------------------- -----------------------
  Function Component      A JavaScript function   All JSX page files
                          that returns UI.        

  JSX                     HTML-like syntax        All components
                          written inside          
                          JavaScript.             

  `return`                Returns the UI from a   All components
                          component.              

  `import`                Brings code from        All files with
                          another file or package dependencies
                          into the current file.  

  `export default`        Makes a component       All page and component
                          available for           files
                          importing.              

  Props                   Passes information from ProductCard
                          parent component to     
                          child component.        

  `BrowserRouter`         Enables client-side     main.jsx
                          routing.                

  `Routes`                Groups route            App.jsx
                          definitions.            

  `Route`                 Connects a URL path to  App.jsx
                          a component.            

  `Link`                  Navigates between       Navbar.jsx and Home.jsx
                          internal routes.        

  `className`             Assigns CSS classes in  All page components
                          JSX.                    

  Fragment `<>`           Groups JSX without an   App.jsx
                          extra HTML element.     
  -----------------------------------------------------------------------

## 8. Suggested teaching order

Teach the project in this order so students understand each concept
before moving forward.

1.  **Project setup:** Vite, npm, folders and files.
2.  **JSX basics:** `function`, `return`, JSX elements and `className`.
3.  **Components:** Create Navbar, Home, About, Products and Contact
    components.
4.  **Import and Export:** Connect components across files.
5.  **CSS:** Import CSS files and style each component separately.
6.  **Props:** Explain the ProductCard component and how the Products
    parent passes data.
7.  **React Router:** Explain BrowserRouter, Routes, Route and Link.
8.  **Testing:** Navigate through all four pages and test the layout.

## 9. Student practice exercises

Ask students to complete these exercises after building the website:

1.  Change the website name from MyStore to StudentStore.
2.  Change the Home page heading and description.
3.  Add another navigation link called Offers.
4.  Add two more products using the ProductCard component.
5.  Change the price of the Laptop.
6.  Add a phone number input to the Contact page.
7.  Change the Navbar background colour.
8.  Add another paragraph to the About page.

## 10. Run the project

Open the VS Code terminal in the project folder:

``` bash
npm run dev
```

Open the URL shown in the terminal.

Test these routes:

  Page       Local URL
  ---------- ----------------------------------
  Home       `http://localhost:5173/`
  About      `http://localhost:5173/about`
  Products   `http://localhost:5173/products`
  Contact    `http://localhost:5173/contact`

------------------------------------------------------------------------

# 11. Common errors and solutions

### Error 1: Failed to resolve import `react-router-dom`

Install the package:

``` bash
npm install react-router-dom
```

### Error 2: Failed to resolve import `./Home.css`

Check that `Home.css` exists inside the `pages` folder and that the
import path is correct.

### Error 3: Component is not defined

Check that the component is imported correctly and that its spelling and
capitalization match the filename and export.

### Error 4: BrowserRouter is already defined or nested

Use `BrowserRouter` only once in `main.jsx`. Do not wrap it again in
`App.jsx`.

### Error 5: Page is blank

Check the terminal and browser console for errors. Verify the import
paths and the JSX syntax.

------------------------------------------------------------------------

## 12. Final teaching summary

By completing this project, students will understand how to:

-   Create a React project using Vite.
-   Build function components.
-   Write JSX.
-   Import and export components.
-   Pass props to reusable components.
-   Add separate CSS files for each page.
-   Navigate between pages using React Router.
-   Organize a small React project using folders.

**Teaching recommendation:** First explain `function`, `return`, JSX,
and `export default` using the Home component. Then teach `ProductCard`
to introduce reusable components and props. Finally, explain React
Router to connect all four pages.
