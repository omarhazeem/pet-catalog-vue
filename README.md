# 🐾 Pet Supplies E-Commerce — Catalog & Discovery

A standalone **Catalog & Discovery microfrontend** for a pet supplies e-commerce platform. This component allows users to browse products, search for products, apply filters, sort results, and view detailed product information.

This project was developed as part of a **Component-Based Software Engineering (CBSE)** group project. Each team member is responsible for an independent microfrontend using a different frontend framework and UI library.

---

## 📌 Project Overview

The e-commerce system is divided into three independent microfrontends:

| Component               | Owner  | Framework | UI Library   |
| ----------------------- | ------ | --------- | ------------ |
| **Catalog & Discovery** | Omar   | Vue 3     | Vuetify 3    |
| **Cart & Checkout**     | Yousef | React     | MUI          |
| **Account & Orders**    | Rahaf  | Lit       | Material Web |

A separate **Shell Application** integrates the three microfrontends into one complete e-commerce application.

---

## 🎯 Catalog & Discovery

The Catalog & Discovery component focuses on helping customers find and explore pet products easily.

The component provides:

* Product browsing
* Live product search
* Product filtering
* Price range filtering
* Product sorting
* Product details
* Stock information
* Responsive product layout
* Empty-state handling

---

## ✨ Features

### 🔎 Product Search

Users can search for products by name.

The product list updates according to the entered search term and displays an empty-state message when no matching products are found.

### 🐾 Product Filtering

Products can be filtered according to:

* Pet category

  * Dogs
  * Cats
  * Birds
  * Accessories
* Brand
* Minimum price
* Maximum price

Filters can be combined to make product discovery easier.

### ↕️ Product Sorting

Products can be sorted according to:

* Most Popular
* Price
* Rating

### 🛍️ Product Grid

Products are displayed in a responsive grid.

Each product card can display:

* Product image
* Product name
* Brand
* Category
* Price
* Rating
* Stock status
* Product badges

Available badges include:

* ⭐ Best Seller
* 🏷️ Sale
* ❌ Out of Stock

### 📋 Product Details

Users can select a product to view additional information through a product details modal.

The modal includes:

* Product name
* Product description
* Price
* Rating
* Stock status
* Product information

### 📭 Empty State

If no products match the current search or filters, the application displays a clear message informing the user that no matching products were found.

---

## 🛠️ Technology Stack

| Technology           | Purpose                           |
| -------------------- | --------------------------------- |
| **Vue 3**            | Frontend framework                |
| **Composition API**  | Component logic                   |
| **`<script setup>`** | Vue component syntax              |
| **Vuetify 3**        | UI components and Material Design |
| **Vite**             | Development server and build tool |
| **JavaScript**       | Application functionality         |
| **HTML/CSS**         | Structure and styling             |

---

## 📁 Project Structure

```text
pet-catalog-vue/
│
├── package.json
├── index.html
│
└── src/
    │
    ├── main.js
    │   └── Application entry point and Vuetify setup
    │
    └── App.vue
        └── Catalog interface
            ├── Search
            ├── Filters
            ├── Sorting
            ├── Product Grid
            └── Product Details Modal
```

---

## ⚙️ Requirements

The following software is required to run the project:

* Node.js
* npm

Check the installed versions using:

```bash
node --version
npm --version
```

---

## 🚀 Installation

Clone or download the repository and open the project directory:

```bash
cd pet-catalog-vue
```

Install the required dependencies:

```bash
npm install
```

---

## ▶️ Running the Project

Start the development server using:

```bash
npm run dev
```

After starting the server, Vite will provide a local URL that can be opened in a web browser.

---

## 📦 Production Build

To create a production build:

```bash
npm run build
```

The production files will be generated in the build output directory.

---

## 🔍 Preview Production Build

To preview the production version locally:

```bash
npm run preview
```

---

## 🧩 Microfrontend Architecture

The project follows a **microfrontend architecture**, where different parts of the e-commerce application are developed independently.

```text
                       E-Commerce Shell
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
      Catalog &          Cart &          Account &
      Discovery          Checkout         Orders
          │                 │                │
        Vue 3             React             Lit
       Vuetify              MUI        Material Web
```

Each microfrontend has its own technology stack and responsibility while being designed to work as part of the complete application.

---

## 🔄 Component Responsibility

### Catalog & Discovery — Omar

Responsible for:

* Product browsing
* Product search
* Product filtering
* Product sorting
* Product cards
* Product details
* Stock status
* Responsive catalog interface

### Cart & Checkout — Yousef

Responsible for:

* Shopping cart
* Cart items
* Quantity management
* Checkout process

### Account & Orders — Rahaf

Responsible for:

* User account
* Account information
* Order history
* Order-related functionality

---

## 📱 Responsive Design

The interface is designed to provide a good user experience across different screen sizes:

* 💻 Desktop
* 📱 Mobile
* 📲 Tablet

The product grid and interface elements adapt to the available screen size.

---

## 🧪 Main User Flow

```text
Open Catalog
     │
     ▼
Browse Products
     │
     ├──── Search by Name
     │
     ├──── Filter by Category
     │
     ├──── Filter by Brand
     │
     ├──── Set Price Range
     │
     └──── Sort Products
                │
                ▼
          Select Product
                │
                ▼
        View Product Details
```

---

## 👥 Team

| Team Member | Component           | Technology         |
| ----------- | ------------------- | ------------------ |
| **Omar**    | Catalog & Discovery | Vue 3 + Vuetify    |
| **Yousef**  | Cart & Checkout     | React + MUI        |
| **Rahaf**   | Account & Orders    | Lit + Material Web |

---

## 🎓 Course Project

This project was developed as part of a **Component-Based Software Engineering (CBSE)** group project.

The project demonstrates the development of independent frontend components using different technologies and their integration within a microfrontend-based e-commerce system.

---

## 📚 References & Acknowledgments

During the development of this project, different technical resources and documentation were consulted to understand and implement the required features and technologies.

The main references included documentation and learning resources related to:

* Vue 3
* Vuetify 3
* Vite
* JavaScript
* Microfrontend Architecture
* Responsive Web Design

These resources were used as references during development, while the implementation and component design were developed according to the requirements of the CBSE group project.

---

## 📄 License

This project was developed for academic purposes as part of the **Component-Based Software Engineering (CBSE)** course project.
