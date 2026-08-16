# Pawfect Pet Supplies — Catalog & Discovery

Part of a microfrontend e-commerce project for a pet supplies store. This repository contains the Catalog & Discovery component, responsible for product browsing, search, filtering, and product details.
Built as an independent, standalone microfrontend as part of a Component-Based Software Engineering (CBSE) group project, where each team member owns one component built with a different framework.

## Role in the system

| Component | Owner | Framework | UI Library |
| :--- | :--- | :--- | :--- |
| **Catalog & Discovery** (this repo) | Omar | Vue 3 | Vuetify |
| **Cart & Checkout** | Yousef | React | MUI |
| **Account & Orders** | Rahaf | Lit | Material Web |

*A separate shell application integrates the three live components together.*

## Features
- Live product search by name
- Filtering by pet category (Dogs, Cats, Birds, Accessories) and brand
- Price range filtering (min/max)
- Sorting (most popular, price, rating)
- Responsive product grid with badges (best seller, sale, out of stock)
- Product details modal with rating, description, and stock status
- Empty-state handling when no products match the current filters

## Tech stack
- Vue 3 (Composition API, `<script setup>`)
- Vuetify 3 for Material Design components
- Vite as the build tool and dev server

## Project structure
```text
pet-catalog-vue/
├── package.json
├── index.html
└── src/
    ├── main.js      # App entry point, Vuetify setup
    └── App.vue      # Catalog UI: search, filters, product grid, details modal
