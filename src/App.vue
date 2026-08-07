<template>
  <v-app>
    <v-app-bar color="white" elevation="1" height="72">
      <v-container class="d-flex align-center">
        <span class="text-h5 font-weight-bold mr-6" style="color:#0d5e51">PawPantry</span>
        <v-text-field
          v-model="searchQuery"
          prepend-inner-icon="mdi-magnify"
          placeholder="Search for food, toys, litter..."
          variant="outlined"
          density="compact"
          hide-details
          clearable
          style="max-width: 340px"
          class="mr-6"
        ></v-text-field>
        <div class="d-none d-md-flex align-center ga-4 mr-auto">
          <span
            v-for="cat in categories.filter(c => c !== 'All')"
            :key="cat"
            class="text-body-2 cursor-pointer"
            :style="selectedCategories.includes(cat) ? 'color:#0d5e51;font-weight:600;border-bottom:2px solid #0d5e51' : 'color:#333'"
            @click="toggleCategory(cat)"
          >{{ cat }}</span>
        </div>
        <v-icon class="mr-4">mdi-heart-outline</v-icon>
        <v-icon>mdi-account-outline</v-icon>
        <v-badge color="orange-darken-2" content="0" class="ml-4">
          <v-icon>mdi-cart-outline</v-icon>
        </v-badge>
      </v-container>
    </v-app-bar>

    <v-main class="bg-white">
      <v-container>
        <p class="text-caption text-grey mt-4">Home / Dogs / Dog Food</p>
        <div class="d-flex align-baseline ga-2 mb-1">
          <h1 class="text-h5 font-weight-bold">Dog Food</h1>
          <span class="text-body-2 text-grey">{{ filteredProducts.length }} products</span>
        </div>

        <v-row class="mt-2">
          <!-- Sidebar Filters -->
          <v-col cols="12" md="3">
            <div class="d-flex justify-space-between align-center mb-2">
              <span class="text-subtitle-1 font-weight-bold">Filters</span>
              <span class="text-caption font-weight-medium" style="color:#0d5e51;cursor:pointer" @click="clearFilters">Clear all</span>
            </div>

            <p class="text-subtitle-2 font-weight-bold mt-3 mb-2">Pet type</p>
            <v-checkbox
              v-for="cat in categories.filter(c => c !== 'All')"
              :key="cat"
              v-model="selectedCategories"
              :label="cat"
              :value="cat"
              density="compact"
              hide-details
              color="teal-darken-4"
            ></v-checkbox>

            <p class="text-subtitle-2 font-weight-bold mt-4 mb-2">Brand</p>
            <v-text-field
              placeholder="Search brands"
              variant="outlined"
              density="compact"
              hide-details
              prepend-inner-icon="mdi-magnify"
              class="mb-2"
            ></v-text-field>
            <v-checkbox
              v-for="brand in brands"
              :key="brand"
              v-model="selectedBrands"
              :label="brand"
              :value="brand"
              density="compact"
              hide-details
              color="teal-darken-4"
            ></v-checkbox>

            <p class="text-subtitle-2 font-weight-bold mt-4 mb-2">Price</p>
            <div class="d-flex ga-2">
              <v-text-field v-model="minPrice" placeholder="$ Min" variant="outlined" density="compact" hide-details type="number"></v-text-field>
              <v-text-field v-model="maxPrice" placeholder="$ Max" variant="outlined" density="compact" hide-details type="number"></v-text-field>
            </div>
          </v-col>

          <!-- Product Grid -->
          <v-col cols="12" md="9">
            <div class="d-flex align-center justify-space-between mb-4 flex-wrap ga-2">
              <div class="d-flex ga-2 align-center flex-wrap">
                <span class="text-caption text-grey">Active:</span>
                <v-chip
                  v-for="brand in selectedBrands"
                  :key="brand"
                  size="small"
                  closable
                  @click:close="selectedBrands = selectedBrands.filter(b => b !== brand)"
                >Brand: {{ brand }}</v-chip>
                <v-chip
                  v-for="cat in selectedCategories"
                  :key="cat"
                  size="small"
                  closable
                  @click:close="selectedCategories = selectedCategories.filter(c => c !== cat)"
                >{{ cat }}</v-chip>
              </div>
              <v-select
                v-model="sortBy"
                :items="['Most popular', 'Price: Low to High', 'Price: High to Low', 'Top rated']"
                variant="outlined"
                density="compact"
                hide-details
                style="max-width: 180px"
              ></v-select>
            </div>

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
                    <v-img :src="product.image" height="150" cover class="bg-grey-lighten-3" :class="{'opacity-60': product.outOfStock}"></v-img>
                    <v-chip
                      v-if="product.badge"
                      size="small"
                      class="position-absolute font-weight-bold"
                      style="top:8px;left:8px"
                      :color="product.badge === 'Best seller' ? 'orange-darken-1' : 'red-darken-2'"
                      text-color="white"
                    >
                      {{ product.badge }}
                    </v-chip>
                    <v-chip
                      v-if="product.outOfStock"
                      size="small"
                      class="position-absolute"
                      style="top:8px;left:8px"
                      color="grey-darken-1"
                      text-color="white"
                    >
                      Out of stock
                    </v-chip>
                    <v-icon class="position-absolute" style="top:8px;right:8px" :color="product.favorited ? 'red' : undefined">
                      {{ product.favorited ? 'mdi-heart' : 'mdi-heart-outline' }}
                    </v-icon>
                  </div>

                  <v-card-text class="flex-grow-1 pb-0">
                    <p class="text-caption text-grey mb-1 text-uppercase">{{ product.brand }}</p>
                    <p class="text-body-2 font-weight-medium mb-1" style="min-height:40px">{{ product.name }}</p>
                    <div class="d-flex align-center ga-1">
                      <v-rating
                        :model-value="product.rating"
                        color="amber"
                        density="compact"
                        half-increments
                        readonly
                        size="x-small"
                      ></v-rating>
                      <span class="text-caption text-grey">({{ product.reviews }})</span>
                    </div>
                    <p class="text-caption text-grey mt-1 mb-0">{{ product.size }}</p>
                    <p class="mt-1 mb-0">
                      <span v-if="product.salePrice" class="font-weight-bold" style="color:#d32f2f">${{ product.salePrice }}</span>
                      <span v-if="product.salePrice" class="text-grey text-decoration-line-through text-caption ml-1">${{ product.price }}</span>
                      <span v-else class="font-weight-bold" style="color:#0d5e51">${{ product.price }}</span>
                    </p>
                  </v-card-text>

                  <v-card-actions class="pt-2">
                    <v-btn
                      v-if="!product.outOfStock"
                      color="#7c4a2d"
                      variant="flat"
                      block
                      rounded="lg"
                      prepend-icon="mdi-cart-outline"
                      @click="openDetails(product)"
                    >
                      Add to Cart
                    </v-btn>
                    <v-btn
                      v-else
                      variant="outlined"
                      color="teal-darken-4"
                      block
                      rounded="lg"
                    >
                      Notify me
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
const selectedBrands = ref([])
const minPrice = ref('')
const maxPrice = ref('')
const sortBy = ref('Most popular')
const categories = ['All', 'Dogs', 'Cats', 'Birds', 'Accessories']
const brands = ['Acana', 'Royal Canin', 'Orijen', "Hill's Science Diet", 'Purina Pro Plan']

const toggleCategory = (cat) => {
  if (selectedCategories.value.includes(cat)) {
    selectedCategories.value = selectedCategories.value.filter(c => c !== cat)
  } else {
    selectedCategories.value.push(cat)
  }
}

const clearFilters = () => {
  selectedCategories.value = []
  selectedBrands.value = []
  minPrice.value = ''
  maxPrice.value = ''
}

const products = ref([
  {
    id: 1,
    name: 'Premium Adult Dog Food (15kg)',
    brand: "Nature's Diet",
    category: 'Dogs',
    size: '15 kg bag',
    price: 49.99,
    salePrice: null,
    badge: 'Best seller',
    outOfStock: false,
    favorited: false,
    rating: 4.5,
    reviews: 342,
    fullDescription: 'Provides complete and balanced nutrition for adult dogs. Formulated with antioxidants, vitamins, and minerals to support digestion and immune health.',
    image: 'https://images.unsplash.com/photo-1589924691995-400dc9ecc119?w=500&q=80'
  },
  {
    id: 2,
    name: 'Interactive Cat Scratching Tree',
    brand: 'Purr Perfect',
    category: 'Cats',
    size: '120 cm tall',
    price: 34.50,
    salePrice: null,
    badge: null,
    outOfStock: false,
    favorited: false,
    rating: 5,
    reviews: 84,
    fullDescription: 'Designed to satisfy your cat\u2019s natural scratching instincts. Features multiple platforms, a hanging ball toy, and a cozy resting shelter.',
    image: 'https://images.unsplash.com/photo-1545249390-6bdfa286032f?w=500&q=80'
  },
  {
    id: 3,
    name: 'Stainless Steel Water Fountain (2L)',
    brand: 'Aqua Pet',
    category: 'Accessories',
    size: '2 liters',
    price: 34.99,
    salePrice: 27.99,
    badge: '20% off',
    outOfStock: false,
    favorited: true,
    rating: 4,
    reviews: 508,
    fullDescription: 'Encourages your pets to drink more water with fresh circulating filtration. Stainless steel top is hygienic and dishwasher safe.',
    image: 'https://images.unsplash.com/photo-1548767797-d8c844163c4c?w=500&q=80'
  },
  {
    id: 4,
    name: 'Natural Wooden Bird Cage Perch Kit',
    brand: 'Professionalism',
    category: 'Birds',
    size: 'Set of 4',
    price: 15.99,
    salePrice: null,
    badge: null,
    outOfStock: true,
    favorited: false,
    rating: 4.5,
    reviews: 96,
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
  let list = products.value.filter((p) => {
    const matchesSearch = p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesCategory = selectedCategories.value.length === 0 || selectedCategories.value.includes(p.category)
    const matchesBrand = selectedBrands.value.length === 0 || selectedBrands.value.includes(p.brand)
    const price = p.salePrice || p.price
    const matchesMin = minPrice.value === '' || price >= Number(minPrice.value)
    const matchesMax = maxPrice.value === '' || price <= Number(maxPrice.value)
    return matchesSearch && matchesCategory && matchesBrand && matchesMin && matchesMax
  })

  if (sortBy.value === 'Price: Low to High') {
    list = [...list].sort((a, b) => (a.salePrice || a.price) - (b.salePrice || b.price))
  } else if (sortBy.value === 'Price: High to Low') {
    list = [...list].sort((a, b) => (b.salePrice || b.price) - (a.salePrice || a.price))
  } else if (sortBy.value === 'Top rated') {
    list = [...list].sort((a, b) => b.rating - a.rating)
  }

  return list
})
</script>
