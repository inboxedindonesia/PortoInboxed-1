<template>
  <div>

    <!-- Navigation Bar -->
    <nav class="navbar" :class="{ scrolled: isScrolled }">
      <div class="container">
        <div class="nav-brand">
          <router-link to="/">
            <h2>LuxeFurniture</h2>
          </router-link>
        </div>
        
        <!-- Mobile Menu Button -->
        <button class="mobile-menu-btn" @click="showMobileMenu = !showMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>

        <ul class="nav-links" :class="{ 'mobile-open': showMobileMenu }">
          <li><router-link to="/" class="nav-link" @click="closeMobileMenu">Home</router-link></li>
          <li><router-link to="/catalog" class="nav-link" @click="closeMobileMenu">Catalog</router-link></li>
          <li><router-link to="/services" class="nav-link" @click="closeMobileMenu">Services</router-link></li>
          <li><router-link to="/about" class="nav-link" @click="closeMobileMenu">About</router-link></li>
          <li><router-link to="/contact" class="nav-link" @click="closeMobileMenu">Contact</router-link></li>
        </ul>
        
        <div class="nav-icons">
          <button class="icon-btn" @click="showCartDropdown = !showCartDropdown">
            🛒
            <span v-if="cart.length > 0" class="cart-count">{{ cart.length }}</span>
          </button>
          <button class="icon-btn">
            ❤️
          </button>
        </div>
      </div>
    </nav>

    <!-- Cart Dropdown -->
    <div v-if="showCartDropdown" class="cart-dropdown">
      <div class="cart-header">
        <h3>Shopping Cart</h3>
        <button @click="showCartDropdown = false" class="close-btn">×</button>
      </div>
      <div v-if="cart.length === 0" class="empty-cart">
        <p>Your cart is empty</p>
      </div>
      <div v-else class="cart-items">
        <div v-for="item in cart" :key="item.id" class="cart-item">
          <img :src="item.image" :alt="item.name" class="item-image">
          <div class="item-details">
            <h4>{{ item.name }}</h4>
            <p class="item-price">${{ item.price }}</p>
            <div class="quantity-controls">
              <button @click="decreaseQuantity(item.id)">-</button>
              <span>{{ item.quantity }}</span>
              <button @click="increaseQuantity(item.id)">+</button>
            </div>
          </div>
          <button @click="removeFromCart(item.id)" class="remove-btn">×</button>
        </div>
      </div>
      <div v-if="cart.length > 0" class="cart-footer">
        <div class="cart-total">
          <strong>Total: ${{ cartTotal }}</strong>
        </div>
        <button class="checkout-btn" @click="proceedToCheckout">
          Proceed to Checkout
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted, onUnmounted } from 'vue'

export default {
  name: 'Header',
  setup() {
    const isScrolled = ref(false)
    const showCartDropdown = ref(false)
    const showMobileMenu = ref(false)
    const cart = ref([])
    
    // Promo bar states
    const showPromo = ref(true)
    const currentPromoIndex = ref(0)
    const promoMessages = ref([
      { message: "🎉 Free Delivery on Orders Over $500! Limited Time Offer" },
      { message: "✨ New Collection: 30% Off Premium Furniture" },
      { message: "🚚 Same Day Delivery Available in Selected Areas" }
    ])
    
    const currentPromo = computed(() => promoMessages.value[currentPromoIndex.value])
    
    const cartTotal = computed(() => {
      return cart.value.reduce((total, item) => total + (item.price * item.quantity), 0)
    })

    const handleScroll = () => {
      isScrolled.value = window.scrollY > 50
    }

    const closeMobileMenu = () => {
      showMobileMenu.value = false
    }

    const closePromo = () => {
      showPromo.value = false
      // Save to localStorage to remember user's choice
      localStorage.setItem('promoBarClosed', 'true')
    }

    const removeFromCart = (itemId) => {
      cart.value = cart.value.filter(item => item.id !== itemId)
    }

    const increaseQuantity = (itemId) => {
      const item = cart.value.find(item => item.id === itemId)
      if (item) {
        item.quantity++
      }
    }

    const decreaseQuantity = (itemId) => {
      const item = cart.value.find(item => item.id === itemId)
      if (item && item.quantity > 1) {
        item.quantity--
      }
    }

    const proceedToCheckout = () => {
      alert('Proceeding to checkout...')
      showCartDropdown.value = false
    }

    // Auto-rotate promo messages
    let promoInterval = null
    const startPromoRotation = () => {
      promoInterval = setInterval(() => {
        currentPromoIndex.value = (currentPromoIndex.value + 1) % promoMessages.value.length
      }, 5000) // Change message every 5 seconds
    }

    const stopPromoRotation = () => {
      if (promoInterval) {
        clearInterval(promoInterval)
        promoInterval = null
      }
    }

    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      
      // Check if user previously closed promo
      const promoClosed = localStorage.getItem('promoBarClosed')
      if (promoClosed === 'true') {
        showPromo.value = false
      } else {
        startPromoRotation()
      }
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
      stopPromoRotation()
    })

    return {
      isScrolled,
      showCartDropdown,
      cart,
      showPromo,
      currentPromo,
      cartTotal,
      handleScroll,
      closePromo,
      removeFromCart,
      increaseQuantity,
      decreaseQuantity,
      proceedToCheckout
    }
  }
}
</script>

<style scoped>
/* Promo Bar Styles */
.promo-bar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 8px 0;
  text-align: center;
  position: relative;
  z-index: 1001;
  font-size: 0.9rem;
  font-weight: 500;
}

.promo-content {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.promo-text {
  display: flex;
  align-items: center;
  gap: 8px;
}

.promo-icon {
  font-size: 1.1rem;
}

.promo-message {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}

.promo-close {
  position: absolute;
  right: 20px;
  background: none;
  border: none;
  color: white;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 4px 8px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.promo-close:hover {
  background: rgba(255, 255, 255, 0.2);
}

/* Navigation Styles */
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

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand a {
  text-decoration: none;
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
  margin: 0;
}

.nav-links {
  display: flex;
  list-style: none;
  align-items: center;
  gap: 0.5rem;
  margin: 0;
  padding: 0;
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
}

.close-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #64748b;
  padding: 4px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.close-btn:hover {
  background: rgba(100, 116, 139, 0.1);
}

.empty-cart {
  padding: 2rem;
  text-align: center;
  color: #7f8c8d;
}

.cart-items {
  padding: 10px;
}

.cart-item {
  display: flex;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid rgba(226, 232, 240, 0.3);
  gap: 15px;
}

.item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 8px;
}

.item-details {
  flex: 1;
}

.item-details h4 {
  margin: 0 0 5px 0;
  font-size: 0.9rem;
  color: #334155;
}

.item-price {
  color: #667eea;
  font-weight: 600;
  margin: 0 0 8px 0;
}

.quantity-controls {
  display: flex;
  align-items: center;
  gap: 8px;
}

.quantity-controls button {
  background: #f1f5f9;
  border: none;
  width: 24px;
  height: 24px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 600;
  color: #475569;
}

.quantity-controls button:hover {
  background: #e2e8f0;
}

.remove-btn {
  background: none;
  border: none;
  color: #ef4444;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 4px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.remove-btn:hover {
  background: rgba(239, 68, 68, 0.1);
}

.cart-footer {
  padding: 20px;
  border-top: 1px solid rgba(226, 232, 240, 0.5);
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.02) 0%, rgba(118, 75, 162, 0.02) 100%);
  border-radius: 0 0 20px 20px;
}

.cart-total {
  text-align: center;
  margin-bottom: 15px;
  font-size: 1.1rem;
  color: #334155;
}

.checkout-btn {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 0.75rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.checkout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .container {
    padding: 0 15px;
  }
  
  .nav-brand h2 {
    font-size: 1.75rem;
  }
  
  .nav-links {
    gap: 0.25rem;
  }
  
  .nav-link {
    padding: 0.75rem 1.25rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 768px) {
  .promo-content {
    padding: 0 15px;
    font-size: 0.9rem;
  }
  
  .promo-close {
    right: 15px;
  }
  
  .container {
    padding: 0 15px;
    position: relative;
  }
  
  .nav-brand h2 {
    font-size: 1.5rem;
  }
  
  .mobile-menu-btn {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    width: 30px;
    height: 30px;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 0;
    z-index: 1001;
  }
  
  .mobile-menu-btn span {
    width: 100%;
    height: 3px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 2px;
    transition: all 0.3s ease;
  }
  
  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 280px;
    height: 100vh;
    background: linear-gradient(135deg, rgba(255, 255, 255, 0.98) 0%, rgba(248, 250, 252, 0.98) 100%);
    backdrop-filter: blur(20px);
    flex-direction: column;
    justify-content: flex-start;
    align-items: stretch;
    padding: 80px 0 20px 0;
    transition: right 0.3s ease;
    box-shadow: -5px 0 25px rgba(0, 0, 0, 0.1);
    z-index: 1000;
  }
  
  .nav-links.mobile-open {
    right: 0;
  }
  
  .nav-links li {
    width: 100%;
  }
  
  .nav-link {
    display: block;
    width: 100%;
    padding: 1rem 2rem;
    border-radius: 0;
    text-align: left;
    border-bottom: 1px solid rgba(226, 232, 240, 0.3);
  }
  
  .nav-link:hover {
    background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
    transform: none;
    box-shadow: none;
  }
  
  .nav-icons {
    gap: 0.5rem;
  }
  
  .icon-btn {
    width: 36px;
    height: 36px;
    font-size: 1rem;
  }
  
  .cart-dropdown {
    right: 10px;
    width: calc(100vw - 20px);
    max-width: 350px;
  }
}

@media (max-width: 480px) {
  .promo-content {
    font-size: 0.85rem;
    padding: 0 10px;
  }
  
  .container {
    padding: 0 10px;
  }
  
  .nav-brand h2 {
    font-size: 1.3rem;
  }
  
  .nav-links {
    width: 100vw;
    right: -100vw;
  }
  
  .nav-links.mobile-open {
    right: 0;
  }
  
  .cart-dropdown {
    right: 5px;
    width: calc(100vw - 10px);
  }
  
  .cart-item {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
  
  .item-image {
    width: 100%;
    height: 120px;
    object-fit: cover;
  }
  
  .item-details {
    width: 100%;
  }
}

/* Hide mobile menu button on desktop */
@media (min-width: 769px) {
  .mobile-menu-btn {
    display: none;
  }
}
</style>