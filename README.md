# Pet Supplies E-Commerce — Catalog & Discovery

This repository contains the **Catalog & Discovery** part of a pet supplies e-commerce website.

The main purpose of this component is to help users browse available pet products, search for a specific product, apply different filters, sort the results, and view more information about each product.

This component is developed as an independent microfrontend as part of a **Component-Based Software Engineering (CBSE)** group project. Each member of the group is responsible for a different part of the system and uses a different frontend framework.

---

## Project Overview

The e-commerce project is divided into three main microfrontends:

| Component               | Owner  | Framework | UI Library   |
| ----------------------- | ------ | --------- | ------------ |
| **Catalog & Discovery** | Omar   | Vue 3     | Vuetify 3    |
| **Cart & Checkout**     | Yousef | React     | MUI          |
| **Account & Orders**    | Rahaf  | Lit       | Material Web |

A separate shell application is used to bring the three components together as one application.

---

## Catalog & Discovery

The Catalog & Discovery component handles the product browsing part of the website.

Users can view products and use different options to find what they are looking for. The component also provides a product details view with information such as the product description, rating, price, and stock status.

### Main responsibilities

* Display products
* Search for products
* Filter products
* Sort products
* Display product information
* Show product availability
* Handle cases where no products match the selected options
* Provide a responsive interface

---

## Features

### Product Search

Users can search for products by entering the product name.

The product list is updated based on the search input, making it easier to find a specific product.

If there are no products that match the search, an empty-state message is displayed.

### Product Categories

Products can be filtered according to their category:

* Dogs
* Cats
* Birds
* Accessories

### Brand Filter

Users can also filter products by brand to make it easier to find products from a specific company.

### Price Filter

The catalog includes a price range filter where users can enter:

* Minimum price
* Maximum price

This allows users to display products within a selected price range.

### Product Sorting

Products can be sorted using different options:

* Most Popular
* Price
* Rating

### Product Cards

Each product is displayed in a product card.

Depending on the product, the card can show:

* Product image
* Product name
* Brand
* Category
* Price
* Rating
* Stock status
* Special badges

The available badges include:

* Best Seller
* Sale
* Out of Stock

### Product Details

Clicking on a product allows the user to view more details in a modal.

The product details include:

* Product name
* Product description
* Price
* Rating
* Stock status
* Other available product information

### Empty State

If the selected search or filters do not return any products, the application displays a message instead of showing an empty product area.

---

## Technologies Used

The project uses the following technologies:

### Vue 3

Vue 3 is used as the main frontend framework for developing the Catalog & Discovery component.

### Composition API

The Composition API is used to organize the component logic and handle the application state.

### Vue `<script setup>`

The `<script setup>` syntax is used to keep Vue components simpler and easier to manage.

### Vuetify 3

Vuetify is used to provide the user interface components and Material Design styling.

### Vite

Vite is used as the development server and build tool for the project.

### JavaScript

JavaScript is used for the application logic, including searching, filtering, sorting, and handling product data.

### HTML & CSS

HTML and CSS are used for the structure and additional styling of the application.

---

## Project Structure

```text id="t1s9q8"
pet-catalog-vue/
│
├── package.json
│
├── index.html
│
└── src/
    │
    ├── main.js
    │
    └── App.vue
```

### `package.json`

Contains the project information, scripts, and required dependencies.

### `index.html`

The main HTML page used as the entry point for the Vue application.

### `src/main.js`

The main entry point of the Vue application.

It is responsible for starting the application and configuring Vuetify.

### `src/App.vue`

Contains the main Catalog & Discovery interface, including:

* Search
* Filters
* Sorting
* Product grid
* Product cards
* Product details modal
* Empty-state handling

---

## Requirements

To run the project locally, the following are required:

* Node.js
* npm

You can check whether they are installed using:

```bash id="y1a8hs"
node --version
npm --version
```

---

## Installation

First, open the project folder:

```bash id="8cl9kf"
cd pet-catalog-vue
```

Then install the project dependencies:

```bash id="8v7gqo"
npm install
```

This will install Vue, Vuetify, Vite, and the other dependencies required by the project.

---

## Running the Project

To start the development server:

```bash id="q4kz8f"
npm run dev
```

After running the command, Vite will display a local address in the terminal. Open this address in a browser to use the application.

---

## Production Build

To create a production version of the project:

```bash id="z6d2ya"
npm run build
```

This creates the files needed for running the project in a production environment.

---

## Preview Production Build

The production build can be tested locally using:

```bash id="c7a2br"
npm run preview
```

---

## Microfrontend Architecture

The project uses a microfrontend approach. Instead of building the whole website as one large application, the system is divided into smaller independent components.

```text id="l6d0ys"
                         E-Commerce Shell
                                |
                ┌───────────────┼───────────────┐
                |               |               |
                ▼               ▼               ▼
       Catalog & Discovery   Cart & Checkout   Account & Orders
                |               |               |
              Vue 3           React             Lit
             Vuetify            MUI        Material Web
```

Each microfrontend has its own framework and UI library.

The Catalog & Discovery component is responsible only for the product browsing and discovery part of the system.

---

## User Flow

The main user flow for the Catalog & Discovery component is:

```text id="xq7g4h"
Open Catalog
     |
     ▼
View Products
     |
     ├── Search by Product Name
     |
     ├── Filter by Category
     |
     ├── Filter by Brand
     |
     ├── Set Price Range
     |
     └── Sort Products
              |
              ▼
        Select a Product
              |
              ▼
       View Product Details
```

This allows the user to find products using different combinations of search, filters, and sorting options.

---

## Responsive Design

The interface is designed to work on different screen sizes.

The layout can be used on:

* Desktop
* Tablet
* Mobile

The product grid and other interface elements adjust according to the available screen size.

---

## Team Responsibilities

| Team Member | Responsibility      | Framework | UI Library   |
| ----------- | ------------------- | --------- | ------------ |
| **Omar**    | Catalog & Discovery | Vue 3     | Vuetify      |
| **Yousef**  | Cart & Checkout     | React     | MUI          |
| **Rahaf**   | Account & Orders    | Lit       | Material Web |

### Omar — Catalog & Discovery

Responsible for:

* Product catalog
* Product search
* Product filtering
* Product sorting
* Product cards
* Product details
* Stock status
* Responsive catalog interface

### Yousef — Cart & Checkout

Responsible for:

* Shopping cart
* Cart items
* Quantity changes
* Checkout functionality

### Rahaf — Account & Orders

Responsible for:

* User account
* Account information
* Order history
* Orders-related functionality

---

## References & Acknowledgments

During the development of the project, documentation and different learning resources were used to understand the technologies and features required for the component.

The main topics referred to were:

* Vue 3 documentation
* Vuetify 3 documentation
* Vite documentation
* JavaScript documentation
* Microfrontend architecture concepts
* Responsive web design

These resources were used to understand the technologies and solve development-related issues while building the project according to the CBSE requirements.

---

## Academic Project

This project was developed as part of a **Component-Based Software Engineering (CBSE)** group project.

The main goal of the project is to build different independent components using different frontend technologies and combine them into one e-commerce system.

---

## License

This project is developed for academic purposes as part of the CBSE course project.
