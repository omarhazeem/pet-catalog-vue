# 🐾 Pet Supplies E-Commerce — Catalog & Discovery

A standalone **Catalog & Discovery** microfrontend for a pet supplies e-commerce platform. This component allows users to browse products, search for products, apply filters, sort results, and view detailed product information.

This project was developed as part of a Component-Based Software Engineering (CBSE) group project. Each team member is responsible for an independent microfrontend using a different frontend framework and UI library.

---

## 📌 Project Overview

The e-commerce system is divided into three independent microfrontends:

| Component | Owner | Framework | UI Library |
| :--- | :--- | :--- | :--- |
| **Catalog & Discovery** | Omar | Vue 3 | Vuetify 3 |
| **Cart & Checkout** | Yousef | React | MUI |
| **Account & Orders** | Rahaf | Lit | Material Web |

*A separate Shell Application integrates the three microfrontends into one complete e-commerce application.*

---

## 🎯 Catalog & Discovery

The Catalog & Discovery component focuses on helping customers find and explore pet products easily.

**The component provides:**
- Product browsing
- Live product search
- Product filtering
- Price range filtering
- Product sorting
- Product details
- Stock information
- Responsive product layout
- Empty-state handling

---

## ✨ Features

### 🔎 Product Search
Users can search for products by name. The product list updates according to the entered search term and displays an empty-state message when no matching products are found.

### 🐾 Product Filtering
Products can be filtered according to:
- **Pet category:** Dogs, Cats, Birds, Accessories
- **Brand**
- **Price range:** Minimum & Maximum price

*Filters can be combined to make product discovery easier.*

### ↕️ Product Sorting
Products can be sorted according to:
- Most Popular
- Price
- Rating

### 🛍️ Product Grid
Products are displayed in a responsive grid. Each product card can display:
- Product image
- Product name
- Brand & Category
- Price & Rating
- Stock status & Product badges

**Available badges include:**
- ⭐ Best Seller
- 🏷️ Sale
- ❌ Out of Stock

### 📋 Product Details
Users can select a product to view additional information through a product details modal. The modal includes:
- Product name & Description
- Price & Rating
- Stock status & Additional product information

### 📭 Empty State
If no products match the current search or filters, the application displays a clear message informing the user that no matching products were found.

---

## 🛠️ Technology Stack

| Technology | Purpose |
| :--- | :--- |
| **Vue 3** | Frontend framework |
| **Composition API** | Component logic |
| `<script setup>` | Vue component syntax |
| **Vuetify 3** | UI components and Material Design |
| **Vite** | Development server and build tool |
| **JavaScript** | Application functionality |
| **HTML / CSS** | Structure and styling |

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
