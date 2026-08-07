<template>
  <v-app>
    <v-app-bar color="white" elevation="1">
      <v-container class="d-flex align-center">
        <span class="text-h5 font-weight-bold" style="color:#0d5e51">PawPantry</span>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="searchQuery"
          prepend-inner-icon="mdi-magnify"
          placeholder="Search for food, toys, etc..."
          variant="outlined"
          density="compact"
          hide-details
          clearable
          style="max-width: 320px"
          class="mr-4"
        ></v-text-field>
        <v-icon class="mr-4">mdi-heart-outline</v-icon>
        <v-icon>mdi-cart-outline</v-icon>
      </v-container>
    </v-app-bar>

    <v-main class="bg-white">
      <v-container>
        <p class="text-caption text-grey mt-4">Home / Search results</p>
        <h1 class="text-h5 font-weight-bold mb-1">
          Results for "{{ searchQuery || 'all products' }}"
          <span class="text-body-2 text-grey font-weight-regular">{{ filteredProducts.length }} products found</span>
        </h1>

        <v-row class="mt-2">
          <!-- Sidebar Filters -->
          <v-col cols="12" md="3">
            <p class="text-subtitle-1 font-weight-bold mb-2">Category</p>
            <v-checkbox
              v-for="cat in categories.filter(c => c !== 'All')"
              :key="cat"
              v-model="selectedCategories"
              :label="cat"
              :value="cat"
              density="compact"
              hide-details
              color="teal-darken-2"
            ></v-checkbox>

            <p class="text-subtitle-1 font-weight-bold mt-4 mb-2">Price</p>
            <div class="d-flex ga-2">
              <v-text-field v-model="minPrice" placeholder="Min" variant="outlined" density="compact" hide-details type="number"></v-text-field>
              <v-text-field v-model="maxPrice" placeholder="Max" variant="outlined" density="compact" hide-details type="number"></v-text-field>
            </div>
          </v-col>

          <!-- Product Grid -->
          <v-col cols="12" md="9">
            <v-row v-if="filteredProducts.length > 0">
              <v-col
                v-for="product in filteredProducts"
                :key="product.id"
                cols="12"
                sm="6"
                md="4"
                lg="3"
              >
                <v-card class="h-100 d-flex flex-column" elevation="0" rounded="lg" style="border:1px solid #e0e0e0">
                  <div class="position-relative">
                    <v-img :src="product.image" height="160" cover class="bg-grey-lighten-3"></v-img>
                    <v-chip
                      v-if="product.badge"
                      size="small"
                      class="position-absolute font-weight-bold"
                      style="top:8px;left:8px"
                      :color="product.badge === 'Sale' ? 'teal-darken-2' : 'orange-darken-1'"
                      text-color="white"
                    >
                      {{ product.badge }}
                    </v-chip>
                    <v-icon class="position-absolute" style="top:8px;right:8px">mdi-heart-outline</v-icon>
                  </div>

                  <v-card-text class="flex-grow-1 pb-0">
                    <p class="text-caption text-grey mb-1">{{ product.category }}</p>
                    <p class="text-body-2 font-weight-medium mb-1" style="min-height:40px">{{ product.name }}</p>
                    <v-rating
                      :model-value="product.rating"
                      color="amber"
                      density="compact"
                      half-increments
                      readonly
                      size="x-small"
                    ></v-rating>
                    <p class="mt-1 mb-0">
                      <span v-if="product.salePrice" class="font-weight-bold" style="color:#d32f2f">${{ product.salePrice }}</span>
                      <span v-if="product.salePrice" class="text-grey text-decoration-line-through text-caption ml-1">${{ product.price }}</span>
                      <span v-else class="font-weight-bold">${{ product.price }}</span>
                    </p>
                  </v-card-text>

                  <v-card-actions class="pt-0">
                    <v-btn
                      color="teal-darken-2"
                      variant="outlined"
                      block
                      rounded="lg"
                      @click="openDetails(product)"
                    >
                      Add to Cart
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-col>
            </v-row>

            <!-- No Results State -->
            <div v-else class="text-center py-12">
              <v-icon size="72" color="grey-lighten-1">mdi-magnify-close</v-icon>
              <h3 class="text-h6 font-weight-bold mt-4">No products found</h3>
              <p class="text-body-2 text-grey">We could not find anything matching your search. Try a different keyword or check the spelling.</p>
            </div>
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
          <v-card-subtitle class="text-h6 font-weight-bold" style="color:#0d5e51">
            Price: ${{ selectedProduct.salePrice || selectedProduct.price }}
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
const selectedCategories = ref([])
const minPrice = ref('')
const maxPrice = ref('')
const categories = ['All', 'Dogs', 'Cats', 'Birds', 'Accessories']

const products = ref([
  {
    id: 1,
    name: 'Premium Adult Dog Food (15kg)',
    category: 'Dogs',
    price: 49.99,
    salePrice: null,
    badge: 'Bestseller',
    rating: 4.5,
    fullDescription: 'Provides complete and balanced nutrition for adult dogs. Formulated with antioxidants, vitamins, and minerals to support digestion and immune health.',
    image: 'https://images.unsplash.com/photo-1589924691995-400dc9ecc119?w=500&q=80'
  },
  {
    id: 2,
    name: 'Interactive Cat Scratching Tree',
    category: 'Cats',
    price: 34.50,
    salePrice: null,
    badge: null,
    rating: 5,
    fullDescription: 'Designed to satisfy your cat\u2019s natural scratching instincts. Features multiple platforms, a hanging ball toy, and a cozy resting shelter.',
    image: 'https://images.unsplash.com/photo-1545249390-6bdfa286032f?w=500&q=80'
  },
  {
    id: 3,
    name: 'Stainless Steel Water Fountain (2L)',
    category: 'Accessories',
    price: 34.99,
    salePrice: 27.99,
    badge: 'Sale',
    rating: 4,
    fullDescription: 'Encourages your pets to drink more water with fresh circulating filtration. Stainless steel top is hygienic and dishwasher safe.',
    image: 'https://images.unsplash.com/photo-1548767797-d8c844163c4c?w=500&q=80'
  },
  {
    id: 4,
    name: 'Natural Wooden Bird Cage Perch Kit',
    category: 'Birds',
    price: 15.99,
    salePrice: null,
    badge: null,
    rating: 4.5,
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
    const matchesSearch = p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesCategory = selectedCategories.value.length === 0 || selectedCategories.value.includes(p.category)
    const price = p.salePrice || p.price
    const matchesMin = minPrice.value === '' || price >= Number(minPrice.value)
    const matchesMax = maxPrice.value === '' || price <= Number(maxPrice.value)
    return matchesSearch && matchesCategory && matchesMin && matchesMax
  })
})
</script>
