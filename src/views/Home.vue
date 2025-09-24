<template>
  <div id="app">
    <!-- Navigation -->
    <nav class="navbar" :class="{ 'scrolled': isScrolled }">
      <div class="container">
        <div class="nav-brand">
          <h2>LuxeFurniture</h2>
        </div>
        <ul class="nav-links">
          <li><router-link to="/" class="nav-link">Home</router-link></li>
          <li><router-link to="/services" class="nav-link">Services</router-link></li>
          <li><router-link to="/catalog" class="nav-link">Catalog</router-link></li>
          <li><a href="#about" class="nav-link">About</a></li>
          <li><a href="#contact" class="nav-link">Contact</a></li>
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

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <div class="hero-text">
          <h1 class="hero-title">Transform Your Space</h1>
          <p class="hero-subtitle">Discover premium furniture that combines elegance, comfort, and functionality</p>
          <div class="hero-buttons">
            <router-link to="/catalog" class="btn btn-primary">Shop Collection</router-link>
            <button class="btn btn-secondary" @click="showVideoModal = true">Watch Story</button>
          </div>
        </div>
        <div class="hero-image">
          <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=800&h=600&fit=crop" alt="Luxury Furniture">
        </div>
      </div>
    </section>

    <!-- Furniture Slider Section -->
    <section class="furniture-slider-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Our Premium Collection</h2>
          <p class="section-subtitle">Explore our finest furniture pieces</p>
        </div>
        
        <div class="slider-container">
          <div class="slider-wrapper" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
            <div v-for="(slide, index) in furnitureSlides" :key="index" class="slide">
              <div class="slide-content">
                <div class="slide-image">
                  <img :src="slide.image" :alt="slide.title" />
                </div>
                <div class="slide-info">
                  <h3>{{ slide.title }}</h3>
                  <p>{{ slide.description }}</p>
                  <span class="slide-price">${{ slide.price.toLocaleString() }}</span>
                  <button class="btn btn-primary" @click="viewProduct(slide)">View Details</button>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Navigation Buttons -->
          <button class="slider-btn prev-btn" @click="prevSlide" :disabled="currentSlide === 0">
            <i class="fas fa-chevron-left"></i>
          </button>
          <button class="slider-btn next-btn" @click="nextSlide" :disabled="currentSlide === furnitureSlides.length - 1">
            <i class="fas fa-chevron-right"></i>
          </button>
          
          <!-- Dots Indicator -->
          <div class="slider-dots">
            <button 
              v-for="(slide, index) in furnitureSlides" 
              :key="index" 
              class="dot" 
              :class="{ active: currentSlide === index }"
              @click="goToSlide(index)"
            ></button>
          </div>
        </div>
      </div>
    </section>

    <!-- Featured Products -->
    <section id="products" class="products-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Featured Collection</h2>
          <p class="section-subtitle">Handpicked pieces that define modern luxury</p>
        </div>
        
        <div class="products-grid">
          <div v-for="product in products" :key="product.id" class="product-card" @click="openQuickView(product)">
            <div class="product-image-container">
              <img :src="product.image" :alt="product.name" class="product-image">
              <div class="product-overlay">
                <button class="btn-quick-view">Quick View</button>
                <button class="btn-wishlist" @click.stop="addToWishlist(product)">♡</button>
              </div>
            </div>
            <div class="product-info">
              <h3 class="product-name">{{ product.name }}</h3>
              <p class="product-price">${{ product.price.toLocaleString() }}</p>
              <div class="product-rating">
                <div class="stars">
                  <span v-for="i in 5" :key="i" class="star" :class="{ 'filled': i <= product.rating }">★</span>
                </div>
                <span class="rating-count">({{ product.reviews }})</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about-section">
      <div class="container">
        <div class="about-content">
          <div class="about-text">
            <h2 class="section-title">Crafting Excellence Since 1985</h2>
            <p class="about-description">
              At LuxeFurniture, we believe that exceptional furniture is more than just functional pieces—it's an expression of your personal style and a reflection of your values. For over three decades, we've been dedicated to creating furniture that combines timeless design with modern functionality.
            </p>
            <div class="about-stats">
              <div class="stat">
                <h3>10,000+</h3>
                <p>Happy Customers</p>
              </div>
              <div class="stat">
                <h3>500+</h3>
                <p>Unique Designs</p>
              </div>
              <div class="stat">
                <h3>35+</h3>
                <p>Years Experience</p>
              </div>
            </div>
          </div>
          <div class="about-image">
            <img src="https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&h=400&fit=crop" alt="Our Workshop">
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section id="services" class="services-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Our Services</h2>
          <p class="section-subtitle">Complete solutions for your furniture needs</p>
        </div>
        
        <div class="services-grid">
          <div class="service-card">
            <div class="service-icon">🏠</div>
            <h3>Interior Design</h3>
            <p>Professional interior design consultation to create your perfect space</p>
          </div>
          <div class="service-card">
            <div class="service-icon">🚚</div>
            <h3>Free Delivery</h3>
            <p>Complimentary delivery and setup for orders over $1,000</p>
          </div>
          <div class="service-card">
            <div class="service-icon">🔧</div>
            <h3>Assembly Service</h3>
            <p>Expert assembly and installation by our trained professionals</p>
          </div>
          <div class="service-card">
            <div class="service-icon">🛡️</div>
            <h3>Warranty</h3>
            <p>Comprehensive warranty coverage on all our furniture pieces</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact-section">
      <div class="container">
        <div class="contact-content">
          <div class="contact-info">
            <h2 class="section-title">Get in Touch</h2>
            <p class="contact-description">Ready to transform your space? Contact us for personalized assistance.</p>
            
            <div class="contact-details">
              <div class="contact-item">
                <div class="contact-icon">📍</div>
                <div>
                  <h4>Visit Our Showroom</h4>
                  <p>123 Design Street, Furniture District<br>New York, NY 10001</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">📞</div>
                <div>
                  <h4>Call Us</h4>
                  <p>(555) 123-4567<br>Mon-Sat: 9AM-7PM</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">✉️</div>
                <div>
                  <h4>Email Us</h4>
                  <p>hello@luxefurniture.com<br>support@luxefurniture.com</p>
                </div>
              </div>
            </div>
          </div>
          
          <div class="contact-form-container">
            <form class="contact-form" @submit.prevent="submitContactForm">
              <div class="form-group">
                <input type="text" v-model="contactForm.name" placeholder="Your Name" required>
              </div>
              <div class="form-group">
                <input type="email" v-model="contactForm.email" placeholder="Your Email" required>
              </div>
              <div class="form-group">
                <input type="tel" v-model="contactForm.phone" placeholder="Your Phone">
              </div>
              <div class="form-group">
                <textarea v-model="contactForm.message" placeholder="Your Message" rows="5" required></textarea>
              </div>
              <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
                <span v-if="isSubmitting">Sending...</span>
                <span v-else>Send Message</span>
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <h3>LuxeFurniture</h3>
            <p>Creating beautiful spaces with premium furniture since 1985.</p>
            <div class="social-links">
              <a href="#" class="social-link">📘</a>
              <a href="#" class="social-link">📷</a>
              <a href="#" class="social-link">🐦</a>
            </div>
          </div>
          <div class="footer-section">
            <h4>Quick Links</h4>
            <ul>
              <li><a href="#home">Home</a></li>
              <li><router-link to="/catalog">Catalog</router-link></li>
              <li><a href="#about">About</a></li>
              <li><a href="#services">Services</a></li>
            </ul>
          </div>
          <div class="footer-section">
            <h4>Categories</h4>
            <ul>
              <li><a href="#">Living Room</a></li>
              <li><a href="#">Bedroom</a></li>
              <li><a href="#">Dining Room</a></li>
              <li><a href="#">Office</a></li>
            </ul>
          </div>
          <div class="footer-section">
            <h4>Customer Service</h4>
            <ul>
              <li><a href="#">Contact Us</a></li>
              <li><a href="#">Shipping Info</a></li>
              <li><a href="#">Returns</a></li>
              <li><a href="#">FAQ</a></li>
            </ul>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2024 LuxeFurniture. All rights reserved.</p>
        </div>
      </div>
    </footer>

    <!-- Quick View Modal -->
    <div v-if="showQuickView" class="modal-overlay" @click="closeQuickView">
      <div class="modal-content" @click.stop>
        <button class="modal-close" @click="closeQuickView">×</button>
        <div class="modal-body">
          <div class="modal-image">
            <img :src="selectedProduct.image" :alt="selectedProduct.name">
          </div>
          <div class="modal-info">
            <h2>{{ selectedProduct.name }}</h2>
            <p class="modal-price">${{ selectedProduct.price?.toLocaleString() }}</p>
            <div class="modal-rating">
              <div class="stars">
                <span v-for="i in 5" :key="i" class="star" :class="{ 'filled': i <= selectedProduct.rating }">★</span>
              </div>
              <span>({{ selectedProduct.reviews }} reviews)</span>
            </div>
            <p class="modal-description">{{ selectedProduct.description }}</p>
            <div class="modal-actions">
              <button class="btn btn-primary" @click="addToCart(selectedProduct)">Add to Cart</button>
              <button class="btn btn-secondary" @click="addToWishlist(selectedProduct)">Add to Wishlist</button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Video Modal -->
    <div v-if="showVideoModal" class="modal-overlay" @click="showVideoModal = false">
      <div class="video-modal" @click.stop>
        <button class="modal-close" @click="showVideoModal = false">×</button>
        <div class="video-container">
          <iframe 
            src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
            frameborder="0" 
            allowfullscreen>
          </iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted, onUnmounted } from 'vue'

export default {
  name: 'Home',
  setup() {
    const isScrolled = ref(false)
    const showQuickView = ref(false)
    const selectedProduct = ref({})
    const wishlist = ref([])
    const showVideoModal = ref(false)
    const cart = ref([])
    const showCartDropdown = ref(false)
    const isSubmitting = ref(false)
    
    // Slider data and state
    const currentSlide = ref(0)
    const furnitureSlides = ref([
      {
        id: 1,
        title: "Luxury Living Room Collection",
        description: "Transform your living space with our premium sofa sets, coffee tables, and entertainment units.",
        price: 4299,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=800&h=500&fit=crop"
      },
      {
        id: 2,
        title: "Modern Dining Experience",
        description: "Elegant dining sets that bring family and friends together for memorable meals.",
        price: 3199,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=800&h=500&fit=crop"
      },
      {
        id: 3,
        title: "Bedroom Sanctuary",
        description: "Create your perfect retreat with our luxurious bedroom furniture collections.",
        price: 5499,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=800&h=500&fit=crop"
      },
      {
        id: 4,
        title: "Executive Office Suite",
        description: "Professional workspace furniture designed for productivity and comfort.",
        price: 2899,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=800&h=500&fit=crop"
      },
      {
        id: 5,
        title: "Outdoor Paradise",
        description: "Weather-resistant outdoor furniture for your patio, garden, or balcony.",
        price: 1899,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=800&h=500&fit=crop"
      },
      {
        id: 6,
        title: "Kids Wonderland Collection",
        description: "Safe, colorful, and fun furniture designed specifically for children's rooms and play areas.",
        price: 2299,
        image: "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&h=500&fit=crop"
      },
      {
        id: 7,
        title: "Vintage Classic Series",
        description: "Timeless vintage-inspired furniture that adds character and elegance to any space.",
        price: 3799,
        image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=800&h=500&fit=crop"
      }
    ])
    
    const contactForm = ref({
      name: '',
      email: '',
      phone: '',
      message: ''
    })

    const products = ref([
      {
        id: 1,
        name: "Meridian Sofa Collection",
        price: 3299,
        rating: 5,
        reviews: 127,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=400&h=300&fit=crop",
        description: "Luxurious modular seating with premium Italian leather"
      },
      {
        id: 2,
        name: "Aurora Dining Set",
        price: 2799,
        rating: 4,
        reviews: 89,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=400&h=300&fit=crop",
        description: "Elegant 8-seater dining table with matching chairs"
      },
      {
        id: 3,
        name: "Serenity Bedroom Suite",
        price: 4199,
        rating: 5,
        reviews: 156,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=400&h=300&fit=crop",
        description: "Complete bedroom set with king-size bed and storage"
      },
      {
        id: 4,
        name: "Executive Office Collection",
        price: 1899,
        rating: 4,
        reviews: 203,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=400&h=300&fit=crop",
        description: "Professional workspace furniture with ergonomic design"
      }
    ])

    const cartTotal = computed(() => {
      return cart.value.reduce((total, item) => total + (item.price * item.quantity), 0)
    })

    const handleScroll = () => {
      isScrolled.value = window.scrollY > 50
    }

    const openQuickView = (product) => {
      selectedProduct.value = product
      showQuickView.value = true
    }

    const closeQuickView = () => {
      showQuickView.value = false
      selectedProduct.value = {}
    }

    const addToCart = (product) => {
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
      
      closeQuickView()
      alert(`${product.name} added to cart!`)
    }

    const removeFromCart = (productId) => {
      const index = cart.value.findIndex(item => item.id === productId)
      if (index > -1) {
        cart.value.splice(index, 1)
      }
    }

    const addToWishlist = (product) => {
      const existingItem = wishlist.value.find(item => item.id === product.id)
      
      if (!existingItem) {
        wishlist.value.push(product)
        alert(`${product.name} added to wishlist!`)
      } else {
        alert(`${product.name} is already in your wishlist!`)
      }
    }

    const proceedToCheckout = () => {
      alert('Proceeding to checkout...')
      showCartDropdown.value = false
    }

    const submitContactForm = async () => {
      isSubmitting.value = true
      
      // Simulate form submission
      await new Promise(resolve => setTimeout(resolve, 2000))
      
      alert('Thank you for your message! We\'ll get back to you soon.')
      
      // Reset form
      contactForm.value = {
        name: '',
        email: '',
        phone: '',
        message: ''
      }
      
      isSubmitting.value = false
    }

    // Slider methods
    const nextSlide = () => {
      if (currentSlide.value < furnitureSlides.value.length - 1) {
        currentSlide.value++
      }
    }

    const prevSlide = () => {
      if (currentSlide.value > 0) {
        currentSlide.value--
      }
    }

    const goToSlide = (index) => {
      currentSlide.value = index
    }

    const viewProduct = (slide) => {
      alert(`Viewing ${slide.title}. Redirecting to product details...`)
    }

    // Auto-play slider
    let sliderInterval = null
    const startAutoPlay = () => {
      sliderInterval = setInterval(() => {
        if (currentSlide.value < furnitureSlides.value.length - 1) {
          currentSlide.value++
        } else {
          currentSlide.value = 0
        }
      }, 4000) // Change slide every 4 seconds
    }

    const stopAutoPlay = () => {
      if (sliderInterval) {
        clearInterval(sliderInterval)
        sliderInterval = null
      }
    }

    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      startAutoPlay()
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
      stopAutoPlay()
    })

    return {
      isScrolled,
      showQuickView,
      selectedProduct,
      wishlist,
      showVideoModal,
      cart,
      showCartDropdown,
      isSubmitting,
      contactForm,
      products,
      cartTotal,
      // Slider variables and methods
      currentSlide,
      furnitureSlides,
      nextSlide,
      prevSlide,
      goToSlide,
      viewProduct,
      // Existing methods
      openQuickView,
      closeQuickView,
      addToCart,
      removeFromCart,
      addToWishlist,
      proceedToCheckout,
      submitContactForm
    }
  }
}
</script>

<style scoped>
/* Global Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  line-height: 1.6;
  color: #333;
}

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
}

.navbar.scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
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
}

.nav-links {
  display: flex;
  list-style: none;
  align-items: center;
  gap: 2rem;
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
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  z-index: 1001;
  max-height: 500px;
  overflow-y: auto;
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid #eee;
}

.close-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #999;
}

.cart-items {
  padding: 20px;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 15px 0;
  border-bottom: 1px solid #f0f0f0;
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
  font-size: 0.9rem;
  margin-bottom: 5px;
}

.cart-item-info p {
  color: #666;
  font-size: 0.8rem;
}

.remove-btn {
  background: #ff4757;
  color: white;
  border: none;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 1rem;
}

.cart-total {
  text-align: center;
  padding: 15px 0;
  border-top: 2px solid #eee;
  margin-top: 15px;
}

.checkout-btn {
  width: 100%;
  background: #667eea;
  color: white;
  border: none;
  padding: 12px;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  margin-top: 10px;
}

.empty-cart {
  padding: 40px 20px;
  text-align: center;
  color: #666;
}

/* Hero Section */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding-top: 80px;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

.hero-subtitle {
  font-size: 1.3rem;
  margin-bottom: 2.5rem;
  opacity: 0.9;
  line-height: 1.6;
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
}

.btn {
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
  text-align: center;
}

.btn-primary {
  background: white;
  color: #667eea;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary:hover {
  background: white;
  color: #667eea;
}

.hero-image img {
  width: 100%;
  height: 500px;
  object-fit: cover;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

/* Furniture Slider Section */
.furniture-slider-section {
  padding: 80px 0;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.slider-container {
  position: relative;
  max-width: 1000px;
  margin: 0 auto;
  overflow: hidden;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.slider-wrapper {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.slide {
  min-width: 100%;
  position: relative;
}

.slide-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 500px;
  background: white;
}

.slide-image {
  position: relative;
  overflow: hidden;
}

.slide-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.slide:hover .slide-image img {
  transform: scale(1.05);
}

.slide-info {
  padding: 60px 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.slide-info h3 {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 20px;
  line-height: 1.2;
}

.slide-info p {
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 30px;
  opacity: 0.9;
}

.slide-price {
  font-size: 2rem;
  font-weight: 700;
  color: #ffd700;
  margin-bottom: 30px;
  display: block;
}

.slide-info .btn {
  align-self: flex-start;
  background: white;
  color: #667eea;
  padding: 15px 30px;
  font-weight: 600;
  border-radius: 50px;
  transition: all 0.3s ease;
}

.slide-info .btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

/* Slider Navigation */
.slider-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.9);
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  color: #667eea;
  transition: all 0.3s ease;
  z-index: 10;
}

.slider-btn:hover {
  background: white;
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.slider-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.prev-btn {
  left: 20px;
}

.next-btn {
  right: 20px;
}

/* Slider Dots */
.slider-dots {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot.active {
  background: white;
  transform: scale(1.2);
}

.dot:hover {
  background: rgba(255, 255, 255, 0.8);
}

/* Products Section */
.products-section {
  padding: 100px 0;
  background: #f8f9fa;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #333;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #666;
  max-width: 600px;
  margin: 0 auto;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.product-card {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
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

.product-card:hover .product-image {
  transform: scale(1.1);
}

.product-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.product-card:hover .product-overlay {
  opacity: 1;
}

.btn-quick-view,
.btn-wishlist {
  background: white;
  border: none;
  padding: 0.8rem 1.5rem;
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
  padding: 1.5rem;
}

.product-name {
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #333;
}

.product-price {
  font-size: 1.3rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 0.5rem;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.stars {
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

.rating-count {
  color: #666;
  font-size: 0.9rem;
}

/* About Section */
.about-section {
  padding: 100px 0;
  background: white;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #666;
  margin-bottom: 2rem;
}

.about-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.stat {
  text-align: center;
}

.stat h3 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 0.5rem;
}

.stat p {
  color: #666;
  font-weight: 500;
}

.about-image img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  border-radius: 20px;
}

/* Services Section */
.services-section {
  padding: 100px 0;
  background: #f8f9fa;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.service-card {
  background: white;
  padding: 2rem;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
}

.service-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.service-card h3 {
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #333;
}

.service-card p {
  color: #666;
  line-height: 1.6;
}

/* Contact Section */
.contact-section {
  padding: 100px 0;
  background: white;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
}

.contact-description {
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.contact-icon {
  font-size: 1.5rem;
  margin-top: 0.2rem;
}

.contact-item h4 {
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #333;
}

.contact-item p {
  color: #666;
  line-height: 1.5;
}

.contact-form {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 20px;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1rem;
  border: 2px solid #e1e5e9;
  border-radius: 10px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

/* Footer */
.footer {
  background: #333;
  color: white;
  padding: 60px 0 20px;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-section h3,
.footer-section h4 {
  margin-bottom: 1rem;
  color: white;
}

.footer-section p {
  color: #ccc;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.footer-section ul {
  list-style: none;
}

.footer-section ul li {
  margin-bottom: 0.5rem;
}

.footer-section ul li a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section ul li a:hover {
  color: #667eea;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: inline-block;
  width: 40px;
  height: 40px;
  background: #667eea;
  color: white;
  text-align: center;
  line-height: 40px;
  border-radius: 50%;
  text-decoration: none;
  transition: background 0.3s ease;
}

.social-link:hover {
  background: #5a6fd8;
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #555;
  color: #ccc;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
}

.modal-content {
  background: white;
  border-radius: 20px;
  max-width: 800px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 20px;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: #999;
  z-index: 1;
}

.modal-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  padding: 2rem;
}

.modal-image img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 15px;
}

.modal-info h2 {
  font-size: 1.8rem;
  margin-bottom: 1rem;
  color: #333;
}

.modal-price {
  font-size: 1.5rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 1rem;
}

.modal-rating {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.modal-description {
  color: #666;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.modal-actions {
  display: flex;
  gap: 1rem;
}

.video-modal {
  background: black;
  border-radius: 10px;
  overflow: hidden;
  max-width: 800px;
  width: 90%;
  position: relative;
}

.video-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
}

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-content,
  .about-content,
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .nav-links {
    gap: 1rem;
  }
  
  .modal-body {
    grid-template-columns: 1fr;
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: flex-start;
  }

  /* Slider responsive */
  .slide-content {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  
  .slide-info {
    padding: 40px 30px;
  }
  
  .slide-info h3 {
    font-size: 2rem;
  }
  
  .slider-btn {
    width: 40px;
    height: 40px;
    font-size: 1rem;
  }
  
  .prev-btn {
    left: 10px;
  }
  
  .next-btn {
    right: 10px;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .nav-links {
    display: none;
  }

  /* Slider mobile */
  .slide-info {
    padding: 30px 20px;
  }
  
  .slide-info h3 {
    font-size: 1.5rem;
  }
  
  .slide-price {
    font-size: 1.5rem;
  }
  
  .furniture-slider-section {
    padding: 40px 0;
  }
}
</style>