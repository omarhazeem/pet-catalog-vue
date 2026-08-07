<template>
  <v-app>
    <v-app-bar color="teal-darken-2" elevation="2">
      <v-app-bar-title class="text-h5 font-weight-bold">
        🐾 Pawfect Pet Supplies - Catalog
      </v-app-bar-title>
    </v-app-bar>

    <v-main class="bg-grey-lighten-4">
      <v-container>
        <!-- Search & Filter Controls -->
        <v-row class="my-4" align="center">
          <v-col cols="12" md="6">
            <v-text-field
              v-model="searchQuery"
              prepend-inner-icon="mdi-magnify"
              label="Search pet food, toys, accessories..."
              variant="outlined"
              hide-details
              clearable
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="6">
            <v-select
              v-model="selectedCategory"
              :items="categories"
              label="Filter by Category"
              variant="outlined"
              hide-details
            ></v-select>
          </v-col>
        </v-row>

        <!-- Product Cards Grid -->
        <v-row>
          <v-col
            v-for="product in filteredProducts"
            :key="product.id"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card class="mx-auto h-100 d-flex flex-column" elevation="2" rounded="lg">
              <v-img :src="product.image" height="200" cover class="align-end text-white">
                <v-chip color="teal-darken-2" class="ma-2 font-weight-bold">
                  ${{ product.price }}
                </v-chip>
              </v-img>

              <v-card-item>
                <v-card-title class="text-subtitle-1 font-weight-bold">
                  {{ product.name }}
                </v-card-title>
                <v-card-subtitle class="mt-1">
                  <v-chip size="x-small" color="secondary" label>
                    {{ product.category }}
                  </v-chip>
                </v-card-subtitle>
              </v-card-item>

              <v-card-text class="flex-grow-1">
                <p class="text-body-2 text-grey-darken-1">{{ product.shortDescription }}</p>
                <v-rating
                  :model-value="product.rating"
                  color="amber"
                  density="compact"
                  half-increments
                  readonly
                  size="small"
                  class="mt-2"
                ></v-rating>
              </v-card-text>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn color="teal-darken-2" variant="elevated" block @click="openDetails(product)">
                  View Details
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

          <!-- Empty State -->
          <v-col v-if="filteredProducts.length === 0" cols="12" class="text-center my-8">
            <v-icon size="64" color="grey">mdi-paw-off</v-icon>
            <h3 class="text-h6 text-grey mt-2">No pet supplies match your search criteria.</h3>
          </v-col>
        </v-row>
      </v-container>

      <!-- Details Dialog Modal -->
      <v-dialog v-model="dialog" max-width="550">
        <v-card v-if="selectedProduct">
          <v-img :src="selectedProduct.image" height="220" cover></v-img>
          <v-card-title class="text-h5 font-weight-bold">
            {{ selectedProduct.name }}
          </v-card-title>
          <v-card-subtitle class="text-h6 text-teal-darken-2 font-weight-bold">
            Price: ${{ selectedProduct.price }}
          </v-card-subtitle>
          <v-card-text>
            <p class="mb-3">{{ selectedProduct.fullDescription }}</p>
            <v-chip color="teal" size="small" class="mr-2">Category: {{ selectedProduct.category }}</v-chip>
            <v-chip color="green" size="small">Status: In Stock</v-chip>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="grey-darken-1" variant="text" @click="dialog = false">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, computed } from 'vue'

const searchQuery = ref('')
const selectedCategory = ref('All')
const categories = ['All', 'Dogs', 'Cats', 'Birds', 'Accessories']

const products = ref([
  {
    id: 1,
    name: 'Premium Adult Dog Food (15kg)',
    category: 'Dogs',
    price: 49.99,
    rating: 4.5,
    shortDescription: 'High-protein formula with real chicken and essential vitamins.',
    fullDescription: 'Provides complete and balanced nutrition for adult dogs. Formulated with antioxidants, vitamins, and minerals to support digestion and immune health.',
    image: 'https://images.unsplash.com/photo-1589924691995-400dc9ecc119?w=500&q=80'
  },
  {
    id: 2,
    name: 'Interactive Cat Scratching Tree',
    category: 'Cats',
    price: 34.50,
    rating: 5,
    shortDescription: 'Multi-level tower with sisal scratching posts and cozy plush condo.',
    fullDescription: 'Designed to satisfy your cat\u2019s natural scratching instincts. Features multiple platforms, a hanging ball toy, and a cozy resting shelter.',
    image: 'https://images.unsplash.com/photo-1545249390-6bdfa286032f?w=500&q=80'
  },
  {
    id: 3,
    name: 'Stainless Steel Water Fountain (2L)',
    category: 'Accessories',
    price: 27.99,
    rating: 4,
    shortDescription: 'Ultra-quiet automatic water dispenser for cats and small dogs.',
    fullDescription: 'Encourages your pets to drink more water with fresh circulating filtration. Stainless steel top is hygienic and dishwasher safe.',
    image: 'https://images.unsplash.com/photo-1548767797-d8c844163c4c?w=500&q=80'
  },
  {
    id: 4,
    name: 'Natural Wooden Bird Cage Perch Kit',
    category: 'Birds',
    price: 15.99,
    rating: 4.5,
    shortDescription: 'Set of 4 natural branch perches for parrots and parakeets.',
    fullDescription: 'Made of 100% natural wood without paint. Easy to attach securely to any wire cage with built-in metal wing nuts.',
    image: 'https://images.unsplash.com/photo-1552728089-57bdde30beb3?w=500&q=80'
  }
])

const dialog = ref(false)
const selectedProduct = ref(null)

const openDetails = (product) => {
  selectedProduct.value = product
  dialog.value = true
}

const filteredProducts = computed(() => {
  return products.value.filter((p) => {
    const matchesSearch = p.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                          p.shortDescription.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesCategory = selectedCategory.value === 'All' || p.category === selectedCategory.value
    return matchesSearch && matchesCategory
  })
})
</script>
