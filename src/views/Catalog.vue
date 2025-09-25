<template>
  <div class="catalog-page">
    <!-- Header Component -->
    <Header />

    <div class="catalog-header elegant-bg">
      <div class="container">
        <div class="catalog-title-section">
          <h1 class="catalog-title">Product Catalog</h1>
          <p class="catalog-subtitle">Discover our complete collection of premium furniture</p>
          <button class="btn-back" @click="$router.push('/')">
            <span>← Back to Home</span>
          </button>
        </div>
      </div>
    </div>

    <div class="catalog-content">
      <div class="container">
        <div class="catalog-layout" :class="{ 'sidebar-hidden': !showSidebar }">
          <!-- Filter Toggle Button -->

          <!-- Filters Sidebar -->
          <div class="filters-sidebar" v-show="showSidebar">
            <div class="filter-section">
              <div class="dropdown-filter">
                <button class="dropdown-toggle" @click="showCategoryDropdown = !showCategoryDropdown">
                  <span>Categories</span>
                  <svg :class="{ 'rotated': showCategoryDropdown }" width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </button>
                <div v-show="showCategoryDropdown" class="dropdown-content">
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="all" @change="filterProducts">
                    <span class="checkmark"></span>
                    All Categories
                  </label>
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="Living Room" @change="filterProducts">
                    <span class="checkmark"></span>
                    Living Room
                  </label>
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="Bedroom" @change="filterProducts">
                    <span class="checkmark"></span>
                    Bedroom
                  </label>
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="Dining Room" @change="filterProducts">
                    <span class="checkmark"></span>
                    Dining Room
                  </label>
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="Office" @change="filterProducts">
                    <span class="checkmark"></span>
                    Office
                  </label>
                  <label class="filter-option">
                    <input type="checkbox" v-model="selectedCategories" value="Outdoor" @change="filterProducts">
                    <span class="checkmark"></span>
                    Outdoor
                  </label>
                </div>
              </div>
            </div>

            <div class="filter-section">
              <h3 class="filter-title">Price Range</h3>
              <div class="price-filter">
                <div class="price-inputs">
                  <input type="number" v-model="priceRange.min" placeholder="Min" @input="filterProducts">
                  <span>-</span>
                  <input type="number" v-model="priceRange.max" placeholder="Max" @input="filterProducts">
                </div>
              </div>
            </div>

            <div class="filter-section">
              <h3 class="filter-title">Rating</h3>
              <div class="rating-filter">
                <label class="rating-option" v-for="rating in [5,4,3,2,1]" :key="rating">
                  <input type="radio" v-model="selectedRating" :value="rating" @change="filterProducts">
                  <span class="rating-stars">
                    <span v-for="i in 5" :key="i" class="star" :class="{ 'filled': i <= rating }">★</span>
                  </span>
                  <span>& up</span>
                </label>
                <label class="rating-option">
                  <input type="radio" v-model="selectedRating" value="0" @change="filterProducts">
                  <span>All Ratings</span>
                </label>
              </div>
            </div>

            <div class="filter-actions">
              <button class="btn-clear-filters" @click="clearFilters">Clear All Filters</button>
            </div>
          </div>

          <!-- Products Grid -->
          <div class="products-grid-container">
            <div class="catalog-controls">
              <div class="results-info">
                <span>Showing {{ filteredCatalogProducts.length }} of {{ catalogProducts.length }} products</span>
              </div>
              
              <!-- Search Box -->
              <div class="search-box">
                <div class="search-input-container">
                  <svg class="search-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="11" cy="11" r="8" stroke="currentColor" stroke-width="2"/>
                    <path d="m21 21-4.35-4.35" stroke="currentColor" stroke-width="2"/>
                  </svg>
                  <input 
                    type="text" 
                    v-model="searchQuery" 
                    placeholder="Search products..." 
                    class="search-input"
                  />
                  <button 
                    v-if="searchQuery" 
                    @click="searchQuery = ''" 
                    class="clear-search"
                  >
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                  </button>
                </div>
              </div>
              
              <button class="sort-controls" @click="showSidebar = !showSidebar">
            <svg v-if="!showSidebar" width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M3 7H21L19 9H5L3 7Z" fill="currentColor"/>
              <path d="M6 12H18L16 14H8L6 12Z" fill="currentColor"/>
              <path d="M9 17H15L13 19H11L9 17Z" fill="currentColor"/>
            </svg>
            <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <span>{{ showSidebar ? 'Hide Filters' : 'Show Filters' }}</span>
          </button>
            </div>

            <div class="catalog-products-grid">
              <div v-for="product in filteredCatalogProducts" :key="product.id" class="catalog-product-card">
                <div class="product-image-container">
                  <img :src="product.image" :alt="product.name" class="product-image">
                  <div class="product-badge" v-if="product.badge">{{ product.badge }}</div>
                  <div class="product-overlay">
                    <button class="btn-quick-view" @click="openCatalogQuickView(product)">Quick View</button>
                    <button class="btn-wishlist" @click="addToCatalogWishlist(product)">
                      <span class="heart-icon">♡</span>
                    </button>
                  </div>
                </div>
                
                <div class="product-info">
                  <div class="product-category">{{ product.category }}</div>
                  <h3 class="product-name">{{ product.name }}</h3>
                  <p class="product-description">{{ product.description }}</p>
                  
                  <div class="product-rating">
                    <div class="stars">
                      <span v-for="i in 5" :key="i" class="star" :class="{ 'filled': i <= product.rating }">★</span>
                    </div>
                    <span class="rating-count">({{ product.reviews }})</span>
                  </div>
                  
                  <div class="product-price">
                    <span class="current-price">${{ product.price.toLocaleString() }}</span>
                    <span class="original-price" v-if="product.originalPrice">${{ product.originalPrice.toLocaleString() }}</span>
                  </div>
                  
                  <div class="product-actions">
                    <button class="btn-add-cart" @click="addToCatalogCart(product)">
                      <span class="cart-icon">🛒</span>
                      Add to Cart
                    </button>
                    <button class="btn-buy-now" @click="buyCatalogProduct(product)">Buy Now</button>
                  </div>
                </div>
              </div>
            </div>

            <div v-if="filteredCatalogProducts.length === 0" class="no-products">
              <div class="no-products-content">
                <div class="no-products-icon">🔍</div>
                <h3>No products found</h3>
                <p>Try adjusting your filters or search criteria</p>
                <button class="btn-clear-filters" @click="clearFilters">Clear All Filters</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Footer Component -->
    <Footer />
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'Catalog',
  components: {
    Header,
    Footer
  },
  setup() {
    // Catalog State
    const selectedCategories = ref(['all'])
    const showCategoryDropdown = ref(false)
    const priceRange = ref({ min: '', max: '' })
    const selectedRating = ref(0)
    const sortBy = ref('name')
    const searchQuery = ref('')
    const cart = ref([])
    const wishlist = ref([])
    const showCartDropdown = ref(false)
    const showSidebar = ref(true)

    // Extended Catalog Products (15 items)
    const catalogProducts = ref([
      {
        id: 1,
        name: "Meridian Sofa Collection",
        category: "Living Room",
        description: "Luxurious modular seating with premium Italian leather",
        price: 3299,
        originalPrice: 3899,
        badge: "Best Seller",
        reviews: 127,
        rating: 5,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=400&h=300&fit=crop"
      },
      {
        id: 2,
        name: "Aurora Dining Set",
        category: "Dining Room",
        description: "Elegant 8-seater dining table with matching chairs",
        price: 2799,
        badge: "New Arrival",
        reviews: 89,
        rating: 4,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=400&h=300&fit=crop"
      },
      {
        id: 3,
        name: "Serenity Bedroom Suite",
        category: "Bedroom",
        description: "Complete bedroom set with king-size bed and storage",
        price: 4199,
        originalPrice: 4799,
        badge: "Limited Edition",
        reviews: 156,
        rating: 5,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=400&h=300&fit=crop"
      },
      {
        id: 4,
        name: "Executive Office Collection",
        category: "Office",
        description: "Professional workspace furniture with ergonomic design",
        price: 1899,
        badge: "Popular",
        reviews: 203,
        rating: 4,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=400&h=300&fit=crop"
      },
      {
        id: 5,
        name: "Zen Garden Lounge",
        category: "Outdoor",
        description: "Weather-resistant outdoor furniture for relaxation",
        price: 2299,
        badge: "Eco-Friendly",
        reviews: 94,
        rating: 4,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=400&h=300&fit=crop"
      },
      {
        id: 6,
        name: "Metropolitan Bar Set",
        category: "Living Room",
        description: "Sophisticated bar furniture for modern entertaining",
        price: 1599,
        badge: "Trending",
        reviews: 78,
        rating: 4,
        image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=400&h=300&fit=crop"
      },
      {
        id: 7,
        name: "Harmony Sectional Sofa",
        category: "Living Room",
        description: "Large sectional sofa perfect for family gatherings",
        price: 2899,
        originalPrice: 3299,
        badge: "Sale",
        reviews: 142,
        rating: 5,
        image: "https://images.unsplash.com/photo-1567538096630-e0c55bd6374c?w=400&h=300&fit=crop"
      },
      {
        id: 8,
        name: "Rustic Farmhouse Table",
        category: "Dining Room",
        description: "Handcrafted wooden dining table with rustic charm",
        price: 1899,
        reviews: 67,
        rating: 4,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=400&h=300&fit=crop"
      },
      {
        id: 9,
        name: "Luxury King Bed Frame",
        category: "Bedroom",
        description: "Upholstered king bed with built-in nightstands",
        price: 2599,
        originalPrice: 2999,
        badge: "Premium",
        reviews: 98,
        rating: 5,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=400&h=300&fit=crop"
      },
      {
        id: 10,
        name: "Modern Office Desk",
        category: "Office",
        description: "Sleek glass-top desk with storage compartments",
        price: 899,
        reviews: 156,
        rating: 4,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=400&h=300&fit=crop"
      },
      {
        id: 11,
        name: "Outdoor Dining Set",
        category: "Outdoor",
        description: "Weather-resistant teak dining set for 6 people",
        price: 1799,
        badge: "Weather-Proof",
        reviews: 73,
        rating: 4,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=400&h=300&fit=crop"
      },
      {
        id: 12,
        name: "Vintage Leather Armchair",
        category: "Living Room",
        description: "Classic leather armchair with brass accents",
        price: 1299,
        originalPrice: 1599,
        badge: "Vintage",
        reviews: 89,
        rating: 5,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=400&h=300&fit=crop"
      },
      {
        id: 13,
        name: "Contemporary Wardrobe",
        category: "Bedroom",
        description: "Spacious wardrobe with mirror doors and LED lighting",
        price: 1999,
        reviews: 112,
        rating: 4,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=400&h=300&fit=crop"
      },
      {
        id: 14,
        name: "Executive Conference Table",
        category: "Office",
        description: "Large conference table for professional meetings",
        price: 3499,
        badge: "Corporate",
        reviews: 45,
        rating: 5,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=400&h=300&fit=crop"
      },
      {
        id: 15,
        name: "Garden Swing Chair",
        category: "Outdoor",
        description: "Comfortable hanging swing chair for outdoor relaxation",
        price: 699,
        badge: "Comfort",
        reviews: 134,
        rating: 4,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=400&h=300&fit=crop"
      }
    ])

    // Computed property for filtered products
    const filteredCatalogProducts = computed(() => {
      let filtered = catalogProducts.value

      // Filter by search query
      if (searchQuery.value.trim() !== '') {
        const query = searchQuery.value.toLowerCase().trim()
        filtered = filtered.filter(product => 
          product.name.toLowerCase().includes(query) ||
          product.description.toLowerCase().includes(query) ||
          product.category.toLowerCase().includes(query)
        )
      }

      // Filter by categories
      if (!selectedCategories.value.includes('all') && selectedCategories.value.length > 0) {
        filtered = filtered.filter(product => 
          selectedCategories.value.includes(product.category)
        )
      }

      // Filter by price range
      if (priceRange.value.min !== '' || priceRange.value.max !== '') {
        filtered = filtered.filter(product => {
          const min = priceRange.value.min === '' ? 0 : Number(priceRange.value.min)
          const max = priceRange.value.max === '' ? Infinity : Number(priceRange.value.max)
          return product.price >= min && product.price <= max
        })
      }

      // Filter by rating
      if (selectedRating.value > 0) {
        filtered = filtered.filter(product => product.rating >= selectedRating.value)
      }

      // Sort products
      switch (sortBy.value) {
        case 'price-low':
          filtered.sort((a, b) => a.price - b.price)
          break
        case 'price-high':
          filtered.sort((a, b) => b.price - a.price)
          break
        case 'rating':
          filtered.sort((a, b) => b.rating - a.rating)
          break
        case 'newest':
          filtered.sort((a, b) => b.id - a.id)
          break
        default:
          filtered.sort((a, b) => a.name.localeCompare(b.name))
      }

      return filtered
    })

    // Methods
    const filterProducts = () => {
      // This method is called when filters change
      // The computed property will automatically update
    }

    const sortProducts = () => {
      // This method is called when sort changes
      // The computed property will automatically update
    }

    const setPriceRange = (min, max) => {
      priceRange.value.min = min
      priceRange.value.max = max
      filterProducts()
    }

    const clearFilters = () => {
      selectedCategories.value = ['all']
      priceRange.value = { min: '', max: '' }
      selectedRating.value = 0
    }

    const addToCatalogCart = (product) => {
      const existingItem = cart.value.find(item => item.id === product.id)
      
      if (existingItem) {
        existingItem.quantity += 1
      } else {
        cart.value.push({
          id: product.id,
          name: product.name,
          price: product.price,
          image: product.image,
          quantity: 1
        })
      }
      
      alert(`${product.name} added to cart!`)
    }

    const buyCatalogProduct = (product) => {
      addToCatalogCart(product)
      // Redirect to checkout or show checkout modal
      alert(`Proceeding to checkout for ${product.name}`)
    }

    const addToCatalogWishlist = (product) => {
      const existingItem = wishlist.value.find(item => item.id === product.id)
      
      if (!existingItem) {
        wishlist.value.push(product)
        alert(`${product.name} added to wishlist!`)
      } else {
        alert(`${product.name} is already in your wishlist!`)
      }
    }

    const openCatalogQuickView = (product) => {
      alert(`Quick view for ${product.name}`)
    }

    // Cart methods
    const cartTotal = computed(() => {
      return cart.value.reduce((total, item) => total + (item.price * item.quantity), 0)
    })

    const removeFromCart = (productId) => {
      cart.value = cart.value.filter(item => item.id !== productId)
    }

    const proceedToCheckout = () => {
      alert('Proceeding to checkout...')
      showCartDropdown.value = false
    }

    return {
      selectedCategories,
      showCategoryDropdown,
      priceRange,
      selectedRating,
      sortBy,
      searchQuery,
      catalogProducts,
      filteredCatalogProducts,
      cart,
      showCartDropdown,
      showSidebar,
      cartTotal,
      filterProducts,
      sortProducts,
      setPriceRange,
      clearFilters,
      addToCatalogCart,
      buyCatalogProduct,
      addToCatalogWishlist,
      openCatalogQuickView,
      removeFromCart,
      proceedToCheckout
    }
  }
}
</script>

<style scoped>
/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Navigation */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(248, 250, 252, 0.95) 100%);
  backdrop-filter: blur(15px);
  z-index: 1000;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 1rem 0;
  border-bottom: 1px solid rgba(226, 232, 240, 0.3);
}

.navbar.scrolled {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.98) 0%, rgba(248, 250, 252, 0.98) 100%);
  box-shadow: 0 4px 32px rgba(0, 0, 0, 0.08);
  border-bottom: 1px solid rgba(226, 232, 240, 0.5);
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand h2 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 800;
  font-size: 2rem;
  letter-spacing: -0.8px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.nav-links {
  display: flex;
  list-style: none;
  align-items: center;
  gap: 0.5rem;
}

.nav-link {
  color: #475569;
  text-decoration: none;
  font-weight: 600;
  padding: 0.875rem 1.5rem;
  border-radius: 50px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  font-size: 0.925rem;
  letter-spacing: 0.2px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.nav-link:hover {
  color: #667eea;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.15);
}

.nav-link.router-link-active {
  color: #ffffff;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  box-shadow: 0 4px 16px rgba(102, 126, 234, 0.3);
}

.nav-icons {
  display: flex;
  gap: 0.75rem;
  align-items: center;
}

.icon-btn {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
  border: 1px solid rgba(102, 126, 234, 0.2);
  font-size: 1.1rem;
  cursor: pointer;
  padding: 0.6rem;
  border-radius: 50%;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  color: #667eea;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-btn:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.25);
  border-color: transparent;
}

.cart-count {
  position: absolute;
  top: -8px;
  right: -8px;
  background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
  color: white;
  border-radius: 50%;
  width: 22px;
  height: 22px;
  font-size: 0.7rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(255, 107, 107, 0.3);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

/* Cart Dropdown */
.cart-dropdown {
  position: fixed;
  top: 80px;
  right: 20px;
  width: 350px;
  background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
  border-radius: 20px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
  z-index: 1001;
  max-height: 500px;
  overflow-y: auto;
  border: 1px solid rgba(226, 232, 240, 0.5);
  animation: slideDown 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid rgba(226, 232, 240, 0.5);
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.05) 0%, rgba(118, 75, 162, 0.05) 100%);
  border-radius: 20px 20px 0 0;
}

.cart-header h3 {
  color: #334155;
  font-weight: 700;
  margin: 0;
  font-size: 1.1rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.3px;
}

.close-btn {
  background: rgba(102, 126, 234, 0.1);
  border: 1px solid rgba(102, 126, 234, 0.2);
  font-size: 1.2rem;
  cursor: pointer;
  color: #667eea;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.close-btn:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  transform: rotate(90deg);
  border-color: transparent;
}

.cart-items {
  max-height: 300px;
  overflow-y: auto;
  padding: 20px;
}

.cart-item {
  display: flex;
  align-items: center;
  padding: 1rem 0;
  border-bottom: 1px solid #f0f0f0;
  gap: 1rem;
}

.cart-item:last-child {
  border-bottom: none;
}

.cart-item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 8px;
}

.cart-item-info {
  flex: 1;
}

.cart-item-info h4 {
  margin: 0 0 0.5rem 0;
  font-size: 0.9rem;
  color: #333;
}

.cart-item-info p {
  margin: 0;
  color: #667eea;
  font-weight: 600;
  font-size: 0.85rem;
}

.remove-btn {
  background: #ff6b6b;
  color: white;
  border: none;
  border-radius: 50%;
  width: 25px;
  height: 25px;
  cursor: pointer;
  font-size: 0.8rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s ease;
}

.remove-btn:hover {
  background: #ff5252;
}

.cart-total {
  padding: 1rem;
  border-top: 1px solid #eee;
  text-align: center;
  font-size: 1.1rem;
  color: #333;
}

.checkout-btn {
  width: calc(100% - 2rem);
  margin: 0 1rem 1rem 1rem;
  background: #667eea;
  color: white;
  border: none;
  padding: 0.75rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.checkout-btn:hover {
  background: #5a67d8;
  transform: translateY(-1px);
}

.empty-cart {
  padding: 2rem;
  text-align: center;
  color: #666;
}

.empty-cart p {
  margin: 0;
}

/* Catalog Page Styles */
.catalog-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
}

.catalog-page::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 80%, rgba(102, 126, 234, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(118, 75, 162, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 40% 40%, rgba(102, 126, 234, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.catalog-header {
  padding: 80px 0 50px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.catalog-header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 30% 70%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 70% 30%, rgba(255, 255, 255, 0.1) 0%, transparent 50%);
  pointer-events: none;
}

.catalog-title-section {
  position: relative;
  z-index: 2;
}

.catalog-title {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.02em;
}

.catalog-subtitle {
  font-size: 1.3rem;
  margin-bottom: 2rem;
  opacity: 0.9;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 400;
}

.btn-back {
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid rgba(255, 255, 255, 0.3);
  color: white;
  padding: 12px 24px;
  border-radius: 50px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(20px);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 500;
  position: relative;
  overflow: hidden;
}

.btn-back::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.6s ease;
}

.btn-back:hover::before {
  left: 100%;
}

.btn-back:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.catalog-content {
  padding: 60px 0;
  position: relative;
  z-index: 2;
}

.catalog-layout {
  display: grid;
  grid-template-columns: 280px 1fr;
  gap: 30px;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
  position: relative;
  transition: grid-template-columns 0.3s ease;
}

.catalog-layout.sidebar-hidden {
  grid-template-columns: 1fr;
}

/* Filter Toggle Button */
.filter-toggle-btn {
  position: absolute;
  top: -50px;
  left: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 25px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  z-index: 10;
}

.filter-toggle-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

.filter-toggle-btn svg {
  transition: transform 0.3s ease;
}

.filter-toggle-btn:hover svg {
  transform: scale(1.1);
}

/* Filters Sidebar */
.filters-sidebar {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  height: fit-content;
  position: sticky;
  top: 20px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  width: 100%;
}

.filters-sidebar:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.12);
}

.filter-section {
  margin-bottom: 18px;
}

.filter-title {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 8px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.filter-options {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

/* Dropdown Filter Styles */
.dropdown-filter {
  position: relative;
}

.dropdown-toggle {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  background: #f8f9fa;
  border: 2px solid #e1e5e9;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: 500;
  color: #2d3748;
  cursor: pointer;
  transition: all 0.3s ease;
}

.dropdown-toggle:hover {
  background: #e9ecef;
  border-color: #667eea;
}

.dropdown-toggle svg {
  transition: transform 0.3s ease;
}

.dropdown-toggle svg.rotated {
  transform: rotate(180deg);
}

.dropdown-content {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: white;
  border: 2px solid #e1e5e9;
  border-radius: 12px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
  z-index: 10;
  margin-top: 4px;
  padding: 8px;
  max-height: 200px;
  overflow-y: auto;
}

/* Header Filter Button Styles */
.header-filter-btn {
  position: static !important;
  top: auto !important;
  left: auto !important;
  margin-bottom: 0 !important;
  width: auto !important;
  min-width: 140px;
}

.filter-option {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 6px 0;
  transition: color 0.3s ease;
}

.filter-option:hover {
  color: #667eea;
}

.filter-option input[type="checkbox"],
.filter-option input[type="radio"] {
  margin-right: 10px;
  accent-color: #667eea;
}

.price-filter {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.price-inputs {
  display: flex;
  align-items: center;
  gap: 8px;
  width: 100%;
}

.price-inputs input {
  flex: 1;
  min-width: 0;
  padding: 8px 10px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  font-size: 0.9rem;
  box-sizing: border-box;
}

.price-inputs span {
  color: #6b7280;
  font-weight: 500;
  flex-shrink: 0;
}

.price-presets {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.price-preset {
  background: #f8f9fa;
  border: 1px solid #e1e5e9;
  padding: 6px 10px;
  border-radius: 6px;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.price-preset:hover {
  background: #667eea;
  color: white;
}

.rating-filter {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.rating-option {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  padding: 4px 0;
}

.rating-stars {
  display: flex;
  gap: 2px;
}

.star {
  color: #ddd;
  font-size: 1rem;
}

.star.filled {
  color: #ffc107;
}

.btn-clear-filters {
  width: 100%;
  background: #dc3545;
  color: white;
  border: none;
  padding: 12px;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.btn-clear-filters:hover {
  background: #c82333;
}

/* Products Grid */
.products-grid-container {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.catalog-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(255, 255, 255, 0.95);
  padding: 20px 30px;
  border-radius: 20px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  gap: 20px;
}

.catalog-controls:hover {
  transform: translateY(-2px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.12);
}

/* Search Box Styles */
.search-box {
  flex: 1;
  max-width: 400px;
}

.search-input-container {
  position: relative;
  display: flex;
  align-items: center;
}

.search-icon {
  position: absolute;
  left: 15px;
  color: #94a3b8;
  z-index: 2;
  pointer-events: none;
}

.search-input {
  width: 100%;
  padding: 12px 45px 12px 45px;
  border: 2px solid rgba(226, 232, 240, 0.5);
  border-radius: 25px;
  font-size: 0.95rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: rgba(255, 255, 255, 0.9);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  outline: none;
}

.search-input:focus {
  border-color: #667eea;
  background: white;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.search-input::placeholder {
  color: #94a3b8;
}

.clear-search {
  position: absolute;
  right: 12px;
  background: none;
  border: none;
  color: #94a3b8;
  cursor: pointer;
  padding: 4px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.clear-search:hover {
  background: rgba(239, 68, 68, 0.1);
  color: #ef4444;
}

.results-info {
  font-weight: 500;
  color: #64748b;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.sort-controls {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 25px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  z-index: 10;
}

.sort-select {
  padding: 10px 15px;
  border: 2px solid rgba(102, 126, 234, 0.2);
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.9);
  font-size: 0.9rem;
  cursor: pointer;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.sort-select:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.catalog-products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 30px;
}

.catalog-product-card {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.catalog-product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
  background: rgba(255, 255, 255, 1);
}

.product-image-container {
  position: relative;
  height: 250px;
  overflow: hidden;
}

.product-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.catalog-product-card:hover .product-image {
  transform: scale(1.1);
}

.product-badge {
  position: absolute;
  top: 15px;
  left: 15px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  backdrop-filter: blur(10px);
}

.product-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.9) 0%, rgba(118, 75, 162, 0.9) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  opacity: 0;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(10px);
}

.catalog-product-card:hover .product-overlay {
  opacity: 1;
}

.btn-quick-view,
.btn-wishlist {
  background: rgba(255, 255, 255, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.3);
  padding: 12px 20px;
  border-radius: 25px;
  cursor: pointer;
  font-weight: 600;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(20px);
  color: #333;
  position: relative;
  overflow: hidden;
}

.btn-quick-view::before,
.btn-wishlist::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(102, 126, 234, 0.2), transparent);
  transition: left 0.5s ease;
}

.btn-quick-view:hover::before,
.btn-wishlist:hover::before {
  left: 100%;
}

.btn-quick-view:hover,
.btn-wishlist:hover {
  background: rgba(255, 255, 255, 1);
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.product-info {
  padding: 25px;
}

.product-category {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 0.85rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 8px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.product-name {
  font-size: 1.3rem;
  font-weight: 700;
  margin-bottom: 8px;
  color: #1e293b;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.3;
}

.product-description {
  color: #64748b;
  font-size: 0.9rem;
  line-height: 1.6;
  margin-bottom: 15px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 15px;
}

.stars {
  display: flex;
  gap: 2px;
}

.rating-count {
  color: #64748b;
  font-size: 0.85rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.product-price {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.current-price {
  font-size: 1.4rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.original-price {
  font-size: 1rem;
  color: #94a3b8;
  text-decoration: line-through;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.product-actions {
  display: flex;
  gap: 10px;
}

.btn-add-cart,
.btn-buy-now {
  flex: 1;
  padding: 12px;
  border: none;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  position: relative;
  overflow: hidden;
}

.btn-add-cart {
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  border: 2px solid rgba(102, 126, 234, 0.2);
}

.btn-add-cart::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(102, 126, 234, 0.1), transparent);
  transition: left 0.5s ease;
}

.btn-add-cart:hover::before {
  left: 100%;
}

.btn-add-cart:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-color: transparent;
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

.btn-buy-now {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: white;
  box-shadow: 0 4px 15px rgba(16, 185, 129, 0.3);
}

.btn-buy-now::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s ease;
}

.btn-buy-now:hover::before {
  left: 100%;
}

.btn-buy-now:hover {
  background: linear-gradient(135deg, #059669 0%, #047857 100%);
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(16, 185, 129, 0.4);
}

.no-products {
  text-align: center;
  padding: 60px 20px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

.no-products-icon {
  font-size: 4rem;
  margin-bottom: 20px;
}

.no-products h3 {
  font-size: 1.5rem;
  margin-bottom: 10px;
  color: #333;
}

.no-products p {
  color: #666;
  margin-bottom: 20px;
}

/* Responsive Design */
@media (max-width: 1200px) {
  .catalog-layout {
    grid-template-columns: 280px 1fr;
    gap: 25px;
  }
  
  .catalog-products-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }
}

@media (max-width: 1024px) {
  .catalog-layout {
    grid-template-columns: 1fr;
    gap: 30px;
  }
  
  .catalog-layout.sidebar-hidden {
    grid-template-columns: 1fr;
  }
  
  .filter-toggle-btn {
    position: relative;
    top: 0;
    margin-bottom: 20px;
    width: fit-content;
  }
  
  .filters-sidebar {
    position: static;
    margin-bottom: 20px;
    max-width: 100%;
  }
  
  .catalog-products-grid {
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 25px;
  }
  
  .catalog-title {
    font-size: 2.8rem;
  }
  
  .catalog-subtitle {
    font-size: 1.1rem;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 15px;
  }
  
  .catalog-hero {
    padding: 120px 0 60px;
  }
  
  .catalog-title {
    font-size: 2.5rem;
    line-height: 1.2;
  }
  
  .catalog-subtitle {
    font-size: 1rem;
  }
  
  .catalog-products-grid {
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
  }
  
  .catalog-controls {
    flex-direction: column;
    gap: 15px;
    text-align: center;
  }
  
  .sort-select,
  .view-toggle {
    width: 100%;
  }
  
  .product-card {
    padding: 1.5rem;
  }
  
  .product-image {
    height: 200px;
  }
  
  .product-title {
    font-size: 1.1rem;
  }
  
  .product-price {
    font-size: 1.3rem;
  }
  
  .filter-group h3 {
    font-size: 1rem;
  }
  
  .filter-option {
    font-size: 0.9rem;
  }
  
  .price-range-inputs {
    flex-direction: column;
    gap: 10px;
  }
  
  .price-input {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 10px;
  }
  
  .catalog-hero {
    padding: 100px 0 40px;
  }
  
  .catalog-title {
    font-size: 2rem;
    line-height: 1.1;
  }
  
  .catalog-subtitle {
    font-size: 0.9rem;
  }
  
  .catalog-products-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }
  
  .product-card {
    padding: 1.25rem;
  }
  
  .product-image {
    height: 180px;
  }
  
  .product-title {
    font-size: 1rem;
  }
  
  .product-price {
    font-size: 1.2rem;
  }
  
  .btn-buy-now {
    padding: 0.75rem 1.5rem;
    font-size: 0.9rem;
  }
  
  .filters-sidebar {
    padding: 1.5rem;
  }
  
  .filter-group {
    margin-bottom: 1.5rem;
  }
  
  .filter-group h3 {
    font-size: 0.95rem;
  }
  
  .filter-option {
    font-size: 0.85rem;
    padding: 8px 0;
  }
  
  .no-products {
    padding: 40px 15px;
  }
  
  .no-products-icon {
    font-size: 3rem;
  }
  
  .no-products h3 {
    font-size: 1.3rem;
  }
}

@media (max-width: 360px) {
  .catalog-title {
    font-size: 1.8rem;
  }
  
  .product-card {
    padding: 1rem;
  }
  
  .product-image {
    height: 160px;
  }
  
  .btn-buy-now {
    padding: 0.6rem 1.2rem;
    font-size: 0.85rem;
  }
}

/* Footer Styles */
.footer {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  position: relative;
  overflow: hidden;
}

.footer-wave {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  overflow: hidden;
  line-height: 0;
  transform: rotate(180deg);
}

.footer-wave svg {
  position: relative;
  display: block;
  width: calc(100% + 1.3px);
  height: 60px;
}

.footer-wave .shape-fill {
  fill: #f8fafc;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 40px;
  padding: 80px 0 40px;
  margin-top: 60px;
}

.footer-brand h3 {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 8px;
  background: linear-gradient(45deg, #fff, #e2e8f0);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.brand-tagline {
  font-size: 0.9rem;
  color: #cbd5e1;
  margin-bottom: 16px;
  font-weight: 500;
}

.footer-brand p {
  color: #e2e8f0;
  line-height: 1.6;
  margin-bottom: 24px;
}

.footer-section h4 {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 20px;
  color: #fff;
}

.footer-section ul {
  list-style: none;
}

.footer-section li {
  margin-bottom: 12px;
}

.footer-section a {
  color: #cbd5e1;
  text-decoration: none;
  transition: color 0.3s ease;
  font-size: 0.95rem;
}

.footer-section a:hover {
  color: #fff;
}

.social-links {
  display: flex;
  gap: 16px;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  color: #cbd5e1;
  text-decoration: none;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.social-link:hover {
  background: rgba(255, 255, 255, 0.2);
  color: #fff;
  transform: translateY(-2px);
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 24px 0;
}

.footer-bottom-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 16px;
}

.footer-bottom p {
  color: #cbd5e1;
  font-size: 0.9rem;
}

.footer-bottom-links {
  display: flex;
  gap: 24px;
}

.footer-bottom-links a {
  color: #cbd5e1;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.3s ease;
}

.footer-bottom-links a:hover {
  color: #fff;
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: 32px;
    padding: 60px 0 32px;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
  }
  
  .footer-bottom-links {
    justify-content: center;
  }
}
</style>