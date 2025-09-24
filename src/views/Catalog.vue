<template>
  <div class="catalog-page">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="container">
        <div class="nav-brand">
          <router-link to="/" class="brand-link">
            <h2>LuxeFurniture</h2>
          </router-link>
        </div>
        <ul class="nav-links">
          <li><router-link to="/" class="nav-link">Home</router-link></li>
          <li><router-link to="/services" class="nav-link">Services</router-link></li>
          <li><router-link to="/catalog" class="nav-link active">Catalog</router-link></li>
          <li><router-link to="/about" class="nav-link">About</router-link></li>
          <li><router-link to="/contact" class="nav-link">Contact</router-link></li>
          <li>
            <div class="nav-icons">
              <button class="icon-btn" @click="showCartDropdown = !showCartDropdown">
                🛒
                <span class="cart-count" v-if="cart.length > 0">{{ cart.length }}</span>
              </button>
              <button class="icon-btn">♡</button>
            </div>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Cart Dropdown -->
    <div v-if="showCartDropdown" class="cart-dropdown">
      <div class="cart-header">
        <h3>Shopping Cart</h3>
        <button @click="showCartDropdown = false" class="close-btn">×</button>
      </div>
      <div class="cart-items" v-if="cart.length > 0">
        <div v-for="item in cart" :key="item.id" class="cart-item">
          <img :src="item.image" :alt="item.name" class="cart-item-image">
          <div class="cart-item-info">
            <h4>{{ item.name }}</h4>
            <p>${{ item.price.toLocaleString() }} x {{ item.quantity }}</p>
          </div>
          <button @click="removeFromCart(item.id)" class="remove-btn">×</button>
        </div>
        <div class="cart-total">
          <strong>Total: ${{ cartTotal.toLocaleString() }}</strong>
        </div>
        <button class="checkout-btn" @click="proceedToCheckout">Proceed to Checkout</button>
      </div>
      <div v-else class="empty-cart">
        <p>Your cart is empty</p>
      </div>
    </div>

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
        <div class="catalog-layout">
          <!-- Filters Sidebar -->
          <div class="filters-sidebar">
            <div class="filter-section">
              <h3 class="filter-title">Categories</h3>
              <div class="filter-options">
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

            <div class="filter-section">
              <h3 class="filter-title">Price Range</h3>
              <div class="price-filter">
                <div class="price-inputs">
                  <input type="number" v-model="priceRange.min" placeholder="Min" @input="filterProducts">
                  <span>-</span>
                  <input type="number" v-model="priceRange.max" placeholder="Max" @input="filterProducts">
                </div>
                <div class="price-presets">
                  <button class="price-preset" @click="setPriceRange(0, 1000)">Under $1,000</button>
                  <button class="price-preset" @click="setPriceRange(1000, 3000)">$1,000 - $3,000</button>
                  <button class="price-preset" @click="setPriceRange(3000, 5000)">$3,000 - $5,000</button>
                  <button class="price-preset" @click="setPriceRange(5000, 999999)">Above $5,000</button>
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
              <div class="sort-controls">
                <select v-model="sortBy" @change="sortProducts" class="sort-select">
                  <option value="name">Sort by Name</option>
                  <option value="price-low">Price: Low to High</option>
                  <option value="price-high">Price: High to Low</option>
                  <option value="rating">Highest Rated</option>
                  <option value="newest">Newest First</option>
                </select>
              </div>
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
  </div>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  name: 'Catalog',
  setup() {
    // Catalog State
    const selectedCategories = ref(['all'])
    const priceRange = ref({ min: '', max: '' })
    const selectedRating = ref(0)
    const sortBy = ref('name')
    const cart = ref([])
    const wishlist = ref([])
    const showCartDropdown = ref(false)

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
      priceRange,
      selectedRating,
      sortBy,
      catalogProducts,
      filteredCatalogProducts,
      cart,
      showCartDropdown,
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
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
  padding: 1rem 0;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand h2 {
  color: #333;
  font-weight: 700;
  font-size: 1.8rem;
  margin: 0;
}

.nav-links {
  display: flex;
  list-style: none;
  align-items: center;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-link {
  color: #333;
  text-decoration: none;
  font-weight: 500;
  padding: 0.5rem 1rem;
  border-radius: 25px;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link:hover,
.nav-link.router-link-active {
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
}

.nav-icons {
  display: flex;
  gap: 1rem;
}

.icon-btn {
  background: none;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: all 0.3s ease;
  position: relative;
}

.icon-btn:hover {
  background: rgba(102, 126, 234, 0.1);
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: #ff4757;
  color: white;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  font-size: 0.7rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Cart Dropdown */
.cart-dropdown {
  position: fixed;
  top: 80px;
  right: 20px;
  width: 350px;
  background: white;
  border-radius: 15px;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
  z-index: 1001;
  border: 1px solid #e1e5e9;
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  border-bottom: 1px solid #eee;
}

.cart-header h3 {
  margin: 0;
  font-size: 1.2rem;
  color: #333;
}

.close-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #666;
  padding: 0;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s ease;
}

.close-btn:hover {
  background: #f0f0f0;
}

.cart-items {
  max-height: 300px;
  overflow-y: auto;
  padding: 1rem;
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
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.catalog-header {
  padding: 120px 0 80px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
}

.catalog-title {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
}

.catalog-subtitle {
  font-size: 1.3rem;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.btn-back {
  background: rgba(255,255,255,0.2);
  border: 2px solid rgba(255,255,255,0.3);
  color: white;
  padding: 12px 24px;
  border-radius: 50px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.btn-back:hover {
  background: rgba(255,255,255,0.3);
  transform: translateY(-2px);
}

.catalog-content {
  padding: 60px 0;
}

.catalog-layout {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 40px;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Filters Sidebar */
.filters-sidebar {
  background: white;
  border-radius: 20px;
  padding: 30px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  height: fit-content;
  position: sticky;
  top: 20px;
}

.filter-section {
  margin-bottom: 30px;
}

.filter-title {
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 15px;
  color: #333;
}

.filter-options {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.filter-option {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 8px 0;
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
  gap: 15px;
}

.price-inputs {
  display: flex;
  align-items: center;
  gap: 10px;
}

.price-inputs input {
  flex: 1;
  padding: 8px 12px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  font-size: 0.9rem;
}

.price-presets {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.price-preset {
  background: #f8f9fa;
  border: 1px solid #e1e5e9;
  padding: 8px 12px;
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
  gap: 8px;
}

.rating-option {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  padding: 5px 0;
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
  background: white;
  padding: 20px 30px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.08);
}

.results-info {
  font-weight: 500;
  color: #666;
}

.sort-select {
  padding: 10px 15px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  background: white;
  font-size: 0.9rem;
  cursor: pointer;
}

.catalog-products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 30px;
}

.catalog-product-card {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
}

.catalog-product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0,0,0,0.15);
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
  background: #667eea;
  color: white;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
}

.product-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.catalog-product-card:hover .product-overlay {
  opacity: 1;
}

.btn-quick-view,
.btn-wishlist {
  background: white;
  border: none;
  padding: 10px 15px;
  border-radius: 25px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-quick-view:hover,
.btn-wishlist:hover {
  background: #667eea;
  color: white;
}

.product-info {
  padding: 25px;
}

.product-category {
  color: #667eea;
  font-size: 0.85rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.product-name {
  font-size: 1.3rem;
  font-weight: 700;
  margin-bottom: 8px;
  color: #333;
}

.product-description {
  color: #666;
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 15px;
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
  color: #666;
  font-size: 0.85rem;
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
  color: #333;
}

.original-price {
  font-size: 1rem;
  color: #999;
  text-decoration: line-through;
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
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-add-cart {
  background: #f8f9fa;
  color: #333;
  border: 2px solid #e1e5e9;
}

.btn-add-cart:hover {
  background: #667eea;
  color: white;
  border-color: #667eea;
}

.btn-buy-now {
  background: #28a745;
  color: white;
}

.btn-buy-now:hover {
  background: #218838;
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
@media (max-width: 1024px) {
  .catalog-layout {
    grid-template-columns: 1fr;
    gap: 30px;
  }
  
  .filters-sidebar {
    position: static;
  }
}

@media (max-width: 768px) {
  .catalog-title {
    font-size: 2.5rem;
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
}
</style>