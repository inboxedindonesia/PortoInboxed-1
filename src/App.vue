<template>
  <div id="app">
    <!-- Navigation -->
    <nav class="navbar" :class="{ 'scrolled': isScrolled }">
      <div class="nav-container">
        <div class="nav-brand">
            <h2 class="brand-text">LuxeFurni</h2>
          </div>
        <ul class="nav-menu">
          <li><a href="#home" class="nav-link">Home</a></li>
          <li><a href="#products" class="nav-link">Products</a></li>
          <li><a href="#about" class="nav-link">About</a></li>
          <li><a href="#contact" class="nav-link">Contact</a></li>
        </ul>
        <div class="nav-cart">
          <button class="cart-btn" @click="toggleCartDropdown">
            <span class="cart-icon">🛒</span>
            <span class="cart-count" v-if="getCartItemCount() > 0">{{ getCartItemCount() }}</span>
          </button>
          <!-- Cart Dropdown -->
          <div class="cart-dropdown" v-if="showCartDropdown" @click.stop>
            <div class="cart-header">
              <h3>Shopping Cart</h3>
              <button class="close-cart" @click="closeCartDropdown">×</button>
            </div>
            <div class="cart-items" v-if="cart.length > 0">
              <div class="cart-item" v-for="item in cart" :key="item.id">
                <img :src="item.image" :alt="item.name" class="cart-item-image">
                <div class="cart-item-info">
                  <h4>{{ item.name }}</h4>
                  <p class="cart-item-price">${{ item.price }}</p>
                  <div class="quantity-controls">
                    <button @click="updateCartQuantity(item.id, item.quantity - 1)">-</button>
                    <span>{{ item.quantity }}</span>
                    <button @click="updateCartQuantity(item.id, item.quantity + 1)">+</button>
                  </div>
                </div>
                <button class="remove-item" @click="removeFromCart(item.id)">×</button>
              </div>
            </div>
            <div class="cart-empty" v-else>
              <p>Your cart is empty</p>
            </div>
            <div class="cart-footer" v-if="cart.length > 0">
              <div class="cart-total">
                <strong>Total: ${{ getCartTotal().toFixed(2) }}</strong>
              </div>
              <button class="checkout-btn" @click="proceedToCheckout">Checkout</button>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-background">
        <div class="floating-shapes">
          <div class="shape shape-1"></div>
          <div class="shape shape-2"></div>
          <div class="shape shape-3"></div>
          <div class="shape shape-4"></div>
          <div class="shape shape-5"></div>
        </div>
      </div>
      
      <div class="hero-content">
        <div class="hero-text">
          <h1 class="hero-title">
            <span class="title-line">Crafting</span>
            <span class="title-line gradient-text">Extraordinary</span>
            <span class="title-line">Living Spaces</span>
          </h1>
          <p class="hero-subtitle">
            Discover premium furniture that transforms your house into a sophisticated sanctuary. 
            Where luxury meets functionality in perfect harmony.
          </p>
          
          <div class="hero-stats">
            <div class="stat-item">
              <span class="stat-number">15K+</span>
              <span class="stat-label">Happy Customers</span>
            </div>
            <div class="stat-item">
              <span class="stat-number">500+</span>
              <span class="stat-label">Premium Products</span>
            </div>
            <div class="stat-item">
              <span class="stat-number">25+</span>
              <span class="stat-label">Years Experience</span>
            </div>
          </div>

          <div class="hero-buttons">
            <button class="btn-primary" @click="exploreCollection">
              <span>Explore Collection</span>
              <div class="btn-glow"></div>
            </button>
            <button class="btn-secondary" @click="watchStory">
              <span>Watch Story</span>
              <div class="play-icon">▶</div>
            </button>
            <button class="btn-contact" @click="showContactForm = true">
              <span>Contact Us</span>
              <div class="contact-icon">✉</div>
            </button>
          </div>
        </div>

        <div class="hero-showcase">
          <div class="showcase-card card-1">
            <div class="card-image">
              <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80" alt="Modern Living Room" />
            </div>
            <div class="card-content">
              <h3>Modern Living</h3>
              <p>Contemporary designs</p>
            </div>
          </div>
          <div class="showcase-card card-2">
            <div class="card-image">
              <img src="https://images.unsplash.com/photo-1555041469-a586c61ea9bc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80" alt="Luxury Sofa" />
            </div>
            <div class="card-content">
              <h3>Luxury Comfort</h3>
              <p>Premium materials</p>
            </div>
          </div>
          <div class="showcase-card card-3">
            <div class="card-image">
              <img src="https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80" alt="Classic Dining Room" />
            </div>
            <div class="card-content">
              <h3>Timeless Style</h3>
              <p>Classic elegance</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Products Section -->
    <section id="products" class="products">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Our Premium Collections</h2>
          <p class="section-subtitle">Curated furniture pieces that define luxury living</p>
        </div>

        <div class="products-grid">
          <div class="product-card" v-for="product in products" :key="product.id">
            <div class="product-image">
              <img :src="product.image" :alt="product.name" />
              <div class="product-badge">{{ product.badge }}</div>
              <div class="product-overlay">
                <button class="quick-view-btn" @click="openQuickView(product)">Quick View</button>
                <button class="wishlist-btn" @click="toggleWishlist(product)" :class="{ 'active': isInWishlist(product) }">
                  {{ isInWishlist(product) ? '♥' : '♡' }}
                </button>
              </div>
            </div>
            <div class="product-info">
              <div class="product-category">{{ product.category }}</div>
              <h3 class="product-name">{{ product.name }}</h3>
              <p class="product-description">{{ product.description }}</p>
              <div class="product-price">
                <span class="current-price">${{ product.price }}</span>
                <span class="original-price" v-if="product.originalPrice">${{ product.originalPrice }}</span>
              </div>
              <div class="product-rating">
                <div class="stars">★★★★★</div>
                <span class="rating-count">({{ product.reviews }})</span>
              </div>
              <button class="btn-add-to-cart" @click="addToCart(product)">Add to Cart</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about">
      <div class="container">
        <div class="about-content">
          <div class="about-text">
            <h2 class="section-title">Crafting Excellence Since 1998</h2>
            <p class="about-description">
              We are passionate artisans dedicated to creating furniture that transcends trends and stands the test of time. 
              Our commitment to quality craftsmanship and innovative design has made us a trusted name in luxury furniture.
            </p>
            
            <div class="about-features">
              <div class="feature-item">
                <div class="feature-icon">🎨</div>
                <div class="feature-content">
                  <h4>Bespoke Design</h4>
                  <p>Custom furniture tailored to your unique vision and space requirements</p>
                </div>
              </div>
              <div class="feature-item">
                <div class="feature-icon">🌿</div>
                <div class="feature-content">
                  <h4>Sustainable Materials</h4>
                  <p>Ethically sourced wood and eco-friendly manufacturing processes</p>
                </div>
              </div>
              <div class="feature-item">
                <div class="feature-icon">⚡</div>
                <div class="feature-content">
                  <h4>Lifetime Warranty</h4>
                  <p>Confidence in our craftsmanship with comprehensive warranty coverage</p>
                </div>
              </div>
            </div>
          </div>

          <div class="about-visual">
            <div class="visual-card main-card">
              <div class="card-content">
                <h3>Master Craftsmen</h3>
                <p>25+ years of expertise</p>
                <div class="card-stats">
                  <div class="stat">
                    <span class="number">98%</span>
                    <span class="label">Satisfaction</span>
                  </div>
                  <div class="stat">
                    <span class="number">15K+</span>
                    <span class="label">Projects</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="visual-card accent-card">
              <div class="card-content">
                <h4>Award Winning</h4>
                <p>Design Excellence 2023</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
      <div class="container">
        <div class="contact-content">
          <div class="contact-info">
            <h2 class="section-title">Let's Create Something Beautiful</h2>
            <p class="contact-description">
              Ready to transform your space? Our design consultants are here to bring your vision to life.
            </p>

            <div class="contact-details">
              <div class="contact-item">
                <div class="contact-icon">📍</div>
                <div class="contact-text">
                  <h4>Showroom Location</h4>
                  <p>123 Design District, Luxury Avenue<br>New York, NY 10001</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">📞</div>
                <div class="contact-text">
                  <h4>Phone & WhatsApp</h4>
                  <p>+1 (555) 123-4567<br>Available 9AM - 8PM EST</p>
                </div>
              </div>
              <div class="contact-item">
                <div class="contact-icon">✉️</div>
                <div class="contact-text">
                  <h4>Email Us</h4>
                  <p>hello@luxefurni.com<br>design@luxefurni.com</p>
                </div>
              </div>
            </div>

            <div class="social-links">
              <a href="#" class="social-link">Instagram</a>
              <a href="#" class="social-link">Pinterest</a>
              <a href="#" class="social-link">Facebook</a>
            </div>
          </div>

          <div class="contact-form">
            <form @submit.prevent="submitForm">
              <div class="form-group">
                <input type="text" placeholder="Your Name" required>
              </div>
              <div class="form-group">
                <input type="email" placeholder="Email Address" required>
              </div>
              <div class="form-group">
                <input type="tel" placeholder="Phone Number">
              </div>
              <div class="form-group">
                <select required>
                  <option value="">Project Budget</option>
                  <option value="5k-15k">$5,000 - $15,000</option>
                  <option value="15k-30k">$15,000 - $30,000</option>
                  <option value="30k-50k">$30,000 - $50,000</option>
                  <option value="50k+">$50,000+</option>
                </select>
              </div>
              <div class="form-group">
                <textarea placeholder="Tell us about your project..." rows="4" required></textarea>
              </div>
              <button type="submit" class="submit-btn">
                <span>Start Your Project</span>
                <div class="btn-arrow">→</div>
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
          <div class="footer-brand">
            <h3>LuxeFurni</h3>
            <p>Crafting extraordinary living spaces with passion and precision since 1998.</p>
          </div>
          <div class="footer-links">
            <div class="link-group">
              <h4>Collections</h4>
              <a href="#">Living Room</a>
              <a href="#">Bedroom</a>
              <a href="#">Dining Room</a>
              <a href="#">Office</a>
            </div>
            <div class="link-group">
              <h4>Services</h4>
              <a href="#">Interior Design</a>
              <a href="#">Custom Furniture</a>
              <a href="#">Consultation</a>
              <a href="#">Delivery</a>
            </div>
            <div class="link-group">
              <h4>Company</h4>
              <a href="#">About Us</a>
              <a href="#">Careers</a>
              <a href="#">Press</a>
              <a href="#">Contact</a>
            </div>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2024 LuxeFurni. All rights reserved.</p>
        </div>
      </div>
    </footer>

    <!-- Quick View Modal -->
    <div v-if="showQuickView" class="modal-overlay" @click="closeQuickView">
      <div class="quick-view-modal" @click.stop>
        <button class="modal-close" @click="closeQuickView">&times;</button>
        <div class="modal-content">
          <div class="modal-image">
            <img :src="selectedProduct.image" :alt="selectedProduct.name" />
          </div>
          <div class="modal-info">
            <div class="product-category">{{ selectedProduct.category }}</div>
            <h2 class="modal-title">{{ selectedProduct.name }}</h2>
            <p class="modal-description">{{ selectedProduct.description }}</p>
            <div class="modal-price">
              <span class="current-price">${{ selectedProduct.price }}</span>
              <span class="original-price" v-if="selectedProduct.originalPrice">${{ selectedProduct.originalPrice }}</span>
            </div>
            <div class="product-rating">
              <div class="stars">★★★★★</div>
              <span class="rating-count">({{ selectedProduct.reviews }} reviews)</span>
            </div>
            <div class="modal-features">
              <h4>Key Features:</h4>
              <ul>
                <li>Premium quality materials</li>
                <li>Expert craftsmanship</li>
                <li>Modern design aesthetic</li>
                <li>Durable construction</li>
                <li>Easy maintenance</li>
              </ul>
            </div>
            <div class="modal-actions">
              <button class="btn-add-cart" @click="addToCart(selectedProduct)">Add to Cart</button>
              <button class="btn-wishlist" @click="toggleWishlist(selectedProduct)" :class="{ 'active': isInWishlist(selectedProduct) }">
                {{ isInWishlist(selectedProduct) ? '♥' : '♡' }} Wishlist
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Video Story Modal -->
    <div v-if="showVideoModal" class="video-modal-overlay" @click="closeVideoModal">
      <div class="video-modal" @click.stop>
        <button class="video-modal-close" @click="closeVideoModal">&times;</button>
        <div class="video-container">
          <iframe 
            width="100%" 
            height="100%" 
            src="https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1&mute=1" 
            title="LuxeFurni Brand Story" 
            frameborder="0" 
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
            allowfullscreen>
          </iframe>
        </div>
        <div class="video-info">
          <h3>Our Craftsmanship Story</h3>
          <p>Discover the passion and dedication behind every piece of LuxeFurni furniture. From traditional techniques to modern innovation.</p>
        </div>
      </div>
    </div>

    <!-- Contact Form Modal -->
    <div v-if="showContactForm" class="modal-overlay" @click="closeContactForm">
      <div class="contact-form-modal" @click.stop>
        <button class="modal-close" @click="closeContactForm">&times;</button>
        <div class="contact-form-content">
          <h2 class="contact-title">Contact Us</h2>
          <p class="contact-subtitle">Get in touch with our team. We'd love to hear from you!</p>
          
          <form @submit.prevent="submitContactForm" class="contact-form">
            <div class="form-group">
              <label for="name">Full Name *</label>
              <input 
                type="text" 
                id="name" 
                v-model="contactForm.name" 
                required 
                placeholder="Enter your full name"
                :class="{ 'error': contactFormErrors.name }"
              />
              <span v-if="contactFormErrors.name" class="error-message">{{ contactFormErrors.name }}</span>
            </div>

            <div class="form-group">
              <label for="email">Email Address *</label>
              <input 
                type="email" 
                id="email" 
                v-model="contactForm.email" 
                required 
                placeholder="Enter your email address"
                :class="{ 'error': contactFormErrors.email }"
              />
              <span v-if="contactFormErrors.email" class="error-message">{{ contactFormErrors.email }}</span>
            </div>

            <div class="form-group">
              <label for="phone">Phone Number</label>
              <input 
                type="tel" 
                id="phone" 
                v-model="contactForm.phone" 
                placeholder="Enter your phone number"
              />
            </div>

            <div class="form-group">
              <label for="subject">Subject *</label>
              <select 
                id="subject" 
                v-model="contactForm.subject" 
                required
                :class="{ 'error': contactFormErrors.subject }"
              >
                <option value="">Select a subject</option>
                <option value="general">General Inquiry</option>
                <option value="product">Product Information</option>
                <option value="order">Order Support</option>
                <option value="custom">Custom Design</option>
                <option value="complaint">Complaint</option>
              </select>
              <span v-if="contactFormErrors.subject" class="error-message">{{ contactFormErrors.subject }}</span>
            </div>

            <div class="form-group">
              <label for="message">Message *</label>
              <textarea 
                id="message" 
                v-model="contactForm.message" 
                required 
                rows="5" 
                placeholder="Tell us how we can help you..."
                :class="{ 'error': contactFormErrors.message }"
              ></textarea>
              <span v-if="contactFormErrors.message" class="error-message">{{ contactFormErrors.message }}</span>
            </div>

            <div class="form-actions">
              <button type="button" class="btn-cancel" @click="closeContactForm">Cancel</button>
              <button type="submit" class="btn-submit" :disabled="isSubmitting">
                <span v-if="!isSubmitting">Send Message</span>
                <span v-else>Sending...</span>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'App',
  setup() {
    const isScrolled = ref(false)
    const showQuickView = ref(false)
    const selectedProduct = ref({})
    const wishlist = ref([])
    const showVideoModal = ref(false)
    const cart = ref([])
    const showCartDropdown = ref(false)
    const showContactForm = ref(false)
    const isSubmitting = ref(false)
    
    const contactForm = ref({
      name: '',
      email: '',
      phone: '',
      subject: '',
      message: ''
    })
    
    const contactFormErrors = ref({
      name: '',
      email: '',
      subject: '',
      message: ''
    })
    
    const products = ref([
      {
        id: 1,
        name: "Meridian Sofa Collection",
        category: "Living Room",
        description: "Luxurious modular seating with premium Italian leather",
        price: "3,299",
        originalPrice: "3,899",
        badge: "Best Seller",
        reviews: 127,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      },
      {
        id: 2,
        name: "Aurora Dining Set",
        category: "Dining Room",
        description: "Elegant 8-seater dining table with matching chairs",
        price: "2,799",
        badge: "New Arrival",
        reviews: 89,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      },
      {
        id: 3,
        name: "Serenity Bedroom Suite",
        category: "Bedroom",
        description: "Complete bedroom set with king-size bed and storage",
        price: "4,199",
        originalPrice: "4,799",
        badge: "Limited Edition",
        reviews: 156,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      },
      {
        id: 4,
        name: "Executive Office Collection",
        category: "Office",
        description: "Professional workspace furniture with ergonomic design",
        price: "1,899",
        badge: "Popular",
        reviews: 203,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      },
      {
        id: 5,
        name: "Zen Garden Lounge",
        category: "Outdoor",
        description: "Weather-resistant outdoor furniture for relaxation",
        price: "2,299",
        badge: "Eco-Friendly",
        reviews: 94,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      },
      {
        id: 6,
        name: "Metropolitan Bar Set",
        category: "Entertainment",
        description: "Sophisticated bar furniture for modern entertaining",
        price: "1,599",
        badge: "Trending",
        reviews: 78,
        image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1000&q=80"
      }
    ])

    const handleScroll = () => {
      isScrolled.value = window.scrollY > 50
    }

    const submitForm = () => {
      alert('Thank you for your interest! We will contact you soon.')
    }

    const openQuickView = (product) => {
      selectedProduct.value = product
      showQuickView.value = true
      document.body.style.overflow = 'hidden'
    }

    const closeQuickView = () => {
      showQuickView.value = false
      document.body.style.overflow = 'auto'
    }

    const toggleWishlist = (product) => {
      const index = wishlist.value.findIndex(item => item.id === product.id)
      if (index > -1) {
        wishlist.value.splice(index, 1)
        // Show notification for removal
        console.log(`${product.name} removed from wishlist`)
      } else {
        wishlist.value.push(product)
        // Show notification for addition
        console.log(`${product.name} added to wishlist`)
      }
    }

    const isInWishlist = (product) => {
      return wishlist.value.some(item => item.id === product.id)
    }

    const exploreCollection = () => {
      const productsSection = document.getElementById('products')
      if (productsSection) {
        productsSection.scrollIntoView({ 
          behavior: 'smooth',
          block: 'start'
        })
      }
    }

    const watchStory = () => {
      // Create and show video modal
      showVideoModal.value = true
      document.body.style.overflow = 'hidden'
    }

    const closeVideoModal = () => {
      showVideoModal.value = false
      document.body.style.overflow = 'auto'
    }

    // Cart management functions
    const addToCart = (product) => {
      const existingItem = cart.value.find(item => item.id === product.id)
      if (existingItem) {
        existingItem.quantity += 1
        console.log(`${product.name} quantity increased to ${existingItem.quantity}`)
      } else {
        cart.value.push({
          ...product,
          quantity: 1
        })
        console.log(`${product.name} added to cart`)
      }
      
      // Automatically open cart dropdown after adding item
      showCartDropdown.value = true
    }

    const removeFromCart = (productId) => {
      const index = cart.value.findIndex(item => item.id === productId)
      if (index > -1) {
        const removedItem = cart.value.splice(index, 1)[0]
        console.log(`${removedItem.name} removed from cart`)
      }
    }

    const updateCartQuantity = (productId, quantity) => {
      const item = cart.value.find(item => item.id === productId)
      if (item) {
        if (quantity <= 0) {
          removeFromCart(productId)
        } else {
          item.quantity = quantity
        }
      }
    }

    const getCartTotal = () => {
      return cart.value.reduce((total, item) => {
        return total + (item.price * item.quantity)
      }, 0)
    }

    const getCartItemCount = () => {
      return cart.value.reduce((total, item) => total + item.quantity, 0)
    }

    const toggleCartDropdown = () => {
      showCartDropdown.value = !showCartDropdown.value
    }

    const closeCartDropdown = () => {
      showCartDropdown.value = false
    }

    // Close cart dropdown when clicking outside
    const handleClickOutside = (event) => {
      if (showCartDropdown.value && !event.target.closest('.nav-cart')) {
        closeCartDropdown()
      }
    }

    // Checkout functionality
    const proceedToCheckout = () => {
      if (cart.value.length === 0) {
        alert('Your cart is empty!')
        return
      }

      const total = getCartTotal()
      const itemCount = getCartItemCount()
      
      // Create checkout summary
      const checkoutSummary = cart.value.map(item => 
        `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`
      ).join('\n')

      // Show checkout confirmation
      const confirmCheckout = confirm(
        `Checkout Summary:\n\n${checkoutSummary}\n\nTotal Items: ${itemCount}\nTotal Amount: $${total.toFixed(2)}\n\nProceed to checkout?`
      )

      if (confirmCheckout) {
        // Simulate checkout process
        alert('Thank you for your purchase! Your order has been placed successfully.')
        
        // Clear cart after successful checkout
        cart.value = []
        closeCartDropdown()
        
        console.log('Checkout completed successfully')
        console.log('Cart cleared')
      }
    }

    // Contact Form Functions
    const closeContactForm = () => {
      showContactForm.value = false
      resetContactForm()
    }

    const resetContactForm = () => {
      contactForm.value = {
        name: '',
        email: '',
        phone: '',
        subject: '',
        message: ''
      }
      contactFormErrors.value = {
        name: '',
        email: '',
        subject: '',
        message: ''
      }
    }

    const validateContactForm = () => {
      let isValid = true
      const errors = {
        name: '',
        email: '',
        subject: '',
        message: ''
      }

      // Validate name
      if (!contactForm.value.name.trim()) {
        errors.name = 'Full name is required'
        isValid = false
      } else if (contactForm.value.name.trim().length < 2) {
        errors.name = 'Name must be at least 2 characters'
        isValid = false
      }

      // Validate email
      if (!contactForm.value.email.trim()) {
        errors.email = 'Email address is required'
        isValid = false
      } else {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
        if (!emailRegex.test(contactForm.value.email)) {
          errors.email = 'Please enter a valid email address'
          isValid = false
        }
      }

      // Validate subject
      if (!contactForm.value.subject) {
        errors.subject = 'Please select a subject'
        isValid = false
      }

      // Validate message
      if (!contactForm.value.message.trim()) {
        errors.message = 'Message is required'
        isValid = false
      } else if (contactForm.value.message.trim().length < 10) {
        errors.message = 'Message must be at least 10 characters'
        isValid = false
      }

      contactFormErrors.value = errors
      return isValid
    }

    const submitContactForm = async () => {
      if (!validateContactForm()) {
        return
      }

      isSubmitting.value = true

      try {
        // Simulate email sending (replace with actual email service)
        await new Promise(resolve => setTimeout(resolve, 2000))

        // Create email content
        const emailContent = {
          to: 'contact@luxefurni.com',
          subject: `Contact Form: ${contactForm.value.subject}`,
          body: `
            Name: ${contactForm.value.name}
            Email: ${contactForm.value.email}
            Phone: ${contactForm.value.phone || 'Not provided'}
            Subject: ${contactForm.value.subject}
            
            Message:
            ${contactForm.value.message}
          `
        }

        console.log('Email would be sent with content:', emailContent)

        // Show success message
        alert('Thank you for your message! We will get back to you within 24 hours.')
        
        // Reset and close form
        closeContactForm()

      } catch (error) {
        console.error('Error sending email:', error)
        alert('Sorry, there was an error sending your message. Please try again later.')
      } finally {
        isSubmitting.value = false
      }
    }

    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      document.addEventListener('click', handleClickOutside)
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
      document.removeEventListener('click', handleClickOutside)
    })

    return {
      isScrolled,
      showQuickView,
      selectedProduct,
      wishlist,
      showVideoModal,
      cart,
      showCartDropdown,
      products,
      submitForm,
      openQuickView,
      closeQuickView,
      toggleWishlist,
      isInWishlist,
      exploreCollection,
      watchStory,
      closeVideoModal,
      addToCart,
      removeFromCart,
      updateCartQuantity,
      getCartTotal,
      getCartItemCount,
      toggleCartDropdown,
      closeCartDropdown,
      proceedToCheckout,
      showContactForm,
      contactForm,
      contactFormErrors,
      isSubmitting,
      closeContactForm,
      submitContactForm
    }
  }
}
</script>

<style>
/* Enhanced Color Palette & Variables */
:root {
  /* Primary Colors - Sophisticated Navy & Gold */
  --primary-navy: #1a2332;
  --primary-gold: #d4af37;
  --primary-cream: #f8f6f0;
  
  /* Secondary Colors - Balanced Earth Tones */
  --secondary-sage: #9caf88;
  --secondary-terracotta: #c17767;
  --secondary-charcoal: #2d3748;
  --secondary-pearl: #f7f5f3;
  
  /* Accent Colors - Refined Highlights */
  --accent-rose-gold: #e8b4a0;
  --accent-forest: #4a5d23;
  --accent-warm-white: #fefcf9;
  --accent-soft-gray: #e2e8f0;
  
  /* Gradients */
  --gradient-primary: linear-gradient(135deg, var(--primary-navy) 0%, var(--secondary-charcoal) 100%);
  --gradient-gold: linear-gradient(135deg, var(--primary-gold) 0%, var(--accent-rose-gold) 100%);
  --gradient-sage: linear-gradient(135deg, var(--secondary-sage) 0%, var(--accent-forest) 100%);
  --gradient-hero: linear-gradient(135deg, var(--primary-cream) 0%, var(--secondary-pearl) 50%, var(--accent-warm-white) 100%);
  
  /* Shadows */
  --shadow-soft: 0 4px 20px rgba(26, 35, 50, 0.08);
  --shadow-medium: 0 8px 30px rgba(26, 35, 50, 0.12);
  --shadow-strong: 0 15px 40px rgba(26, 35, 50, 0.15);
  --shadow-glow: 0 0 30px rgba(212, 175, 55, 0.3);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  line-height: 1.6;
  color: var(--primary-navy);
  background-color: var(--accent-warm-white);
  overflow-x: hidden;
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
  z-index: 1000;
  padding: 20px 0;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  background: rgba(248, 246, 240, 0.8);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(212, 175, 55, 0.1);
}

.navbar.scrolled {
  padding: 15px 0;
  background: rgba(248, 246, 240, 0.95);
  box-shadow: var(--shadow-soft);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.brand-text {
  font-size: 28px;
  font-weight: 700;
  background: var(--gradient-gold);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 40px;
}

.nav-link {
  text-decoration: none;
  color: var(--primary-navy);
  font-weight: 500;
  font-size: 16px;
  position: relative;
  transition: all 0.3s ease;
}

.nav-link:hover {
  color: var(--primary-gold);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--gradient-gold);
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

/* Hero Section */
.hero {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  background: var(--gradient-hero);
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  opacity: 0.6;
  animation: float 20s infinite ease-in-out;
}

.shape-1 {
  width: 120px;
  height: 120px;
  background: var(--gradient-gold);
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 80px;
  height: 80px;
  background: var(--gradient-sage);
  top: 60%;
  right: 15%;
  animation-delay: -5s;
}

.shape-3 {
  width: 150px;
  height: 150px;
  background: linear-gradient(135deg, var(--accent-rose-gold), var(--secondary-terracotta));
  bottom: 30%;
  left: 5%;
  animation-delay: -10s;
}

.shape-4 {
  width: 60px;
  height: 60px;
  background: var(--gradient-primary);
  top: 40%;
  right: 30%;
  animation-delay: -15s;
}

.shape-5 {
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, var(--secondary-sage), var(--primary-gold));
  bottom: 20%;
  right: 10%;
  animation-delay: -7s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  25% { transform: translateY(-20px) rotate(90deg); }
  50% { transform: translateY(-40px) rotate(180deg); }
  75% { transform: translateY(-20px) rotate(270deg); }
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.hero-title {
  font-size: 4.5rem;
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 30px;
}

.title-line {
  display: block;
  animation: slideInUp 1s ease-out forwards;
  opacity: 0;
  transform: translateY(50px);
}

.title-line:nth-child(1) { animation-delay: 0.2s; }
.title-line:nth-child(2) { animation-delay: 0.4s; }
.title-line:nth-child(3) { animation-delay: 0.6s; }

.gradient-text {
  background: var(--gradient-gold);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@keyframes slideInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-subtitle {
  font-size: 1.3rem;
  color: var(--secondary-charcoal);
  margin-bottom: 40px;
  line-height: 1.6;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.8s forwards;
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-stats {
  display: flex;
  gap: 40px;
  margin-bottom: 50px;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1s forwards;
}

.stat-item {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--primary-gold);
  line-height: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--secondary-charcoal);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.hero-buttons {
  display: flex;
  gap: 20px;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
}

.btn-primary, .btn-secondary {
  position: relative;
  padding: 18px 35px;
  border: none;
  border-radius: 50px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  overflow: hidden;
  display: flex;
  align-items: center;
  gap: 10px;
}

.btn-primary {
  background: var(--gradient-gold);
  color: white;
  box-shadow: var(--shadow-medium);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-glow);
}

.btn-secondary {
  background: transparent;
  color: var(--primary-navy);
  border: 2px solid var(--primary-navy);
}

.btn-secondary:hover {
  background: var(--primary-navy);
  color: white;
  transform: translateY(-3px);
}

.btn-glow {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
  transition: left 0.6s;
}

.btn-primary:hover .btn-glow {
  left: 100%;
}

.play-icon {
  width: 20px;
  height: 20px;
  background: var(--primary-navy);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 10px;
  transition: all 0.3s ease;
}

.btn-secondary:hover .play-icon {
  background: white;
  color: var(--primary-navy);
}

.hero-showcase {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  opacity: 0;
  animation: fadeInRight 1s ease-out 1.4s forwards;
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.showcase-card {
  background: white;
  border-radius: 20px;
  padding: 25px;
  box-shadow: var(--shadow-soft);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.showcase-card:hover {
  transform: translateY(-10px);
  box-shadow: var(--shadow-strong);
}

.showcase-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--gradient-gold);
  transform: scaleX(0);
  transition: transform 0.4s ease;
}

.showcase-card:hover::before {
  transform: scaleX(1);
}

.card-1 { grid-column: 1 / -1; }
.card-2, .card-3 { margin-top: 20px; }

.card-image {
  width: 100%;
  height: 120px;
  border-radius: 15px;
  margin-bottom: 20px;
  position: relative;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  border-radius: 15px;
  transition: transform 0.4s ease;
}

.showcase-card:hover .card-image img {
  transform: scale(1.1);
}

/* Remove individual card background styles since we now use images */

.card-content h3 {
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--primary-navy);
  margin-bottom: 8px;
}

.card-content p {
  color: var(--secondary-charcoal);
  font-size: 0.95rem;
}

/* Products Section */
.products {
  padding: 120px 0;
  background: var(--accent-warm-white);
}

.section-header {
  text-align: center;
  margin-bottom: 80px;
}

.section-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--primary-navy);
  margin-bottom: 20px;
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 4px;
  background: var(--gradient-gold);
  border-radius: 2px;
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--secondary-charcoal);
  max-width: 600px;
  margin: 0 auto;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 40px;
}

.product-card {
  background: white;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: var(--shadow-soft);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.product-card:hover {
  transform: translateY(-15px);
  box-shadow: var(--shadow-strong);
}

.product-image {
  height: 280px;
  position: relative;
  overflow: hidden;
  background: var(--gradient-primary);
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.product-card:hover .product-image img {
  transform: scale(1.15);
}

/* Remove individual product card background styles since we now use images */

.product-badge {
  position: absolute;
  top: 20px;
  left: 20px;
  background: var(--gradient-gold);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  z-index: 2;
}

.product-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(26, 35, 50, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  opacity: 0;
  transition: all 0.4s ease;
}

.product-card:hover .product-overlay {
  opacity: 1;
}

.quick-view-btn, .wishlist-btn {
  background: white;
  border: none;
  padding: 12px 20px;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  transform: translateY(20px);
}

.product-card:hover .quick-view-btn,
.product-card:hover .wishlist-btn {
  transform: translateY(0);
}

.quick-view-btn:hover {
  background: var(--primary-gold);
  color: white;
}

.wishlist-btn {
  width: 45px;
  padding: 12px;
  font-size: 18px;
  position: relative;
  overflow: hidden;
}

.wishlist-btn:hover {
  background: var(--secondary-sage);
  color: white;
  transform: translateY(0) scale(1.1);
}

.wishlist-btn.active {
  background: var(--primary-gold);
  color: white;
  animation: heartBeat 0.6s ease-in-out;
}

.wishlist-btn.active:hover {
  background: var(--secondary-terracotta);
  transform: translateY(0) scale(1.15);
}

@keyframes heartBeat {
  0% { transform: translateY(0) scale(1); }
  25% { transform: translateY(0) scale(1.3); }
  50% { transform: translateY(0) scale(1.1); }
  75% { transform: translateY(0) scale(1.25); }
  100% { transform: translateY(0) scale(1.1); }
}

.product-info {
  padding: 30px;
}

.product-category {
  color: var(--primary-gold);
  font-size: 0.9rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 10px;
}

.product-name {
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--primary-navy);
  margin-bottom: 12px;
}

.product-description {
  color: var(--secondary-charcoal);
  margin-bottom: 20px;
  line-height: 1.5;
}

.product-price {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 15px;
}

.current-price {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-gold);
}

.original-price {
  font-size: 1.1rem;
  color: var(--secondary-charcoal);
  text-decoration: line-through;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 10px;
}

.stars {
  color: var(--primary-gold);
  font-size: 1.1rem;
}

.rating-count {
  color: var(--secondary-charcoal);
  font-size: 0.9rem;
}

/* About Section */
.about {
  padding: 120px 0;
  background: var(--secondary-pearl);
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.about-description {
  font-size: 1.2rem;
  color: var(--secondary-charcoal);
  margin-bottom: 50px;
  line-height: 1.7;
}

.about-features {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.feature-item {
  display: flex;
  gap: 20px;
  align-items: flex-start;
}

.feature-icon {
  font-size: 2rem;
  width: 60px;
  height: 60px;
  background: var(--gradient-gold);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.feature-content h4 {
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--primary-navy);
  margin-bottom: 8px;
}

.feature-content p {
  color: var(--secondary-charcoal);
  line-height: 1.6;
}

.about-visual {
  position: relative;
}

.visual-card {
  background: white;
  border-radius: 25px;
  padding: 40px;
  box-shadow: var(--shadow-medium);
  position: relative;
}

.main-card {
  background: var(--gradient-primary);
  color: white;
  border: 2px solid var(--primary-gold);
}

.main-card h3 {
  font-size: 1.8rem;
  margin-bottom: 10px;
  color: var(--primary-gold);
  font-weight: 700;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.main-card p {
  opacity: 1;
  margin-bottom: 30px;
  color: white;
  font-size: 1.1rem;
  font-weight: 500;
  text-shadow: 0 1px 2px rgba(0,0,0,0.3);
}

.card-stats {
  display: flex;
  gap: 40px;
}

.stat .number {
  display: block;
  font-size: 2rem;
  font-weight: 700;
  color: var(--primary-gold);
}

.stat .label {
  font-size: 0.9rem;
  opacity: 0.8;
}

.accent-card {
  position: absolute;
  top: -30px;
  right: -30px;
  background: var(--gradient-gold);
  color: white;
  padding: 25px;
  transform: rotate(5deg);
  box-shadow: var(--shadow-strong);
  z-index: 10;
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  animation: floatCard 3s ease-in-out infinite;
}

@keyframes floatCard {
  0%, 100% {
    transform: rotate(5deg) translateY(0px);
  }
  50% {
    transform: rotate(3deg) translateY(-10px);
  }
}

.accent-card:hover {
  transform: rotate(0deg) translateY(-15px) scale(1.05);
  box-shadow: 0 20px 40px rgba(212, 175, 55, 0.3);
}

.accent-card h4 {
  font-size: 1.2rem;
  margin-bottom: 5px;
}

/* Contact Section */
.contact {
  padding: 120px 0;
  background: var(--accent-warm-white);
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
}

.contact-description {
  font-size: 1.2rem;
  color: var(--secondary-charcoal);
  margin-bottom: 50px;
  line-height: 1.7;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 30px;
  margin-bottom: 40px;
}

.contact-item {
  display: flex;
  gap: 20px;
  align-items: flex-start;
}

.contact-icon {
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  background: var(--gradient-sage);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.contact-text h4 {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--primary-navy);
  margin-bottom: 5px;
}

.contact-text p {
  color: var(--secondary-charcoal);
  line-height: 1.5;
}

.social-links {
  display: flex;
  gap: 20px;
}

.social-link {
  color: var(--primary-navy);
  text-decoration: none;
  font-weight: 500;
  padding: 10px 20px;
  border: 2px solid var(--accent-soft-gray);
  border-radius: 25px;
  transition: all 0.3s ease;
}

.social-link:hover {
  background: var(--primary-gold);
  color: white;
  border-color: var(--primary-gold);
}

.contact-form {
  background: white;
  padding: 50px;
  border-radius: 25px;
  box-shadow: var(--shadow-medium);
}

.form-group {
  margin-bottom: 25px;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 18px 20px;
  border: 2px solid var(--accent-soft-gray);
  border-radius: 15px;
  font-size: 16px;
  font-family: inherit;
  transition: all 0.3s ease;
  background: var(--accent-warm-white);
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary-gold);
  box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
}

.submit-btn {
  width: 100%;
  background: var(--gradient-gold);
  color: white;
  border: none;
  padding: 20px;
  border-radius: 15px;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  transition: all 0.4s ease;
  position: relative;
  overflow: hidden;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-glow);
}

.btn-arrow {
  font-size: 20px;
  transition: transform 0.3s ease;
}

.submit-btn:hover .btn-arrow {
  transform: translateX(5px);
}

/* Quick View Modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(26, 35, 50, 0.8);
  backdrop-filter: blur(10px);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.quick-view-modal {
  background: white;
  border-radius: 25px;
  max-width: 900px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  box-shadow: var(--shadow-strong);
  animation: modalSlideIn 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes modalSlideIn {
  from {
    opacity: 0;
    transform: scale(0.9) translateY(20px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 20px;
  background: var(--accent-soft-gray);
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  z-index: 10;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-close:hover {
  background: var(--primary-gold);
  color: white;
}

.modal-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
}

.modal-image {
  height: 400px;
  overflow: hidden;
  border-radius: 25px 0 0 25px;
}

.modal-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-info {
  padding: 40px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.modal-title {
  font-size: 2rem;
  font-weight: 700;
  color: var(--primary-navy);
  margin-bottom: 15px;
}

.modal-description {
  color: var(--secondary-charcoal);
  margin-bottom: 25px;
  line-height: 1.6;
}

.modal-price {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.modal-features {
  margin-bottom: 30px;
}

.modal-features h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--primary-navy);
  margin-bottom: 15px;
}

.modal-features ul {
  list-style: none;
  padding: 0;
}

.modal-features li {
  color: var(--secondary-charcoal);
  margin-bottom: 8px;
  position: relative;
  padding-left: 20px;
}

.modal-features li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: var(--primary-gold);
  font-weight: bold;
}

.modal-actions {
  display: flex;
  gap: 15px;
}

.btn-add-cart {
  flex: 1;
  background: var(--gradient-gold);
  color: white;
  border: none;
  padding: 15px 25px;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-add-cart:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-medium);
}

.btn-wishlist {
  background: transparent;
  border: 2px solid var(--accent-soft-gray);
  color: var(--primary-navy);
  padding: 15px 20px;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 8px;
  position: relative;
  overflow: hidden;
}

.btn-wishlist:hover {
  border-color: var(--primary-gold);
  color: var(--primary-gold);
  transform: translateY(-2px);
}

.btn-wishlist.active {
  background: var(--primary-gold);
  border-color: var(--primary-gold);
  color: white;
  animation: modalHeartBeat 0.6s ease-in-out;
}

.btn-wishlist.active:hover {
  background: var(--secondary-terracotta);
  border-color: var(--secondary-terracotta);
  transform: translateY(-2px) scale(1.05);
}

@keyframes modalHeartBeat {
  0% { transform: translateY(0) scale(1); }
  25% { transform: translateY(-2px) scale(1.1); }
  50% { transform: translateY(0) scale(1.05); }
  75% { transform: translateY(-2px) scale(1.08); }
  100% { transform: translateY(-2px) scale(1.05); }
}

@media (max-width: 768px) {
  .modal-content {
    grid-template-columns: 1fr;
  }
  
  .modal-image {
    height: 250px;
    border-radius: 25px 25px 0 0;
  }
  
  .modal-info {
    padding: 30px;
  }
  
  .modal-actions {
    flex-direction: column;
  }
}

/* Footer */
.footer {
  background: var(--primary-navy);
  color: white;
  padding: 80px 0 30px;
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 60px;
  margin-bottom: 50px;
}

.footer-brand h3 {
  font-size: 2rem;
  margin-bottom: 20px;
  background: var(--gradient-gold);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-brand p {
  opacity: 0.8;
  line-height: 1.6;
}

.footer-links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}

.link-group h4 {
  font-size: 1.2rem;
  margin-bottom: 20px;
  color: var(--primary-gold);
}

.link-group a {
  display: block;
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  margin-bottom: 12px;
  transition: all 0.3s ease;
}

.link-group a:hover {
  color: var(--primary-gold);
  transform: translateX(5px);
}

.footer-bottom {
  text-align: center;
  padding-top: 30px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  opacity: 0.6;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    gap: 40px;
    text-align: center;
  }
  
  .hero-title {
    font-size: 3rem;
  }
  
  .hero-stats {
    justify-content: center;
  }
  
  .hero-buttons {
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .about-content,
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .products-grid {
    grid-template-columns: 1fr;
  }
  
  .nav-menu {
    display: none;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .footer-links {
    grid-template-columns: 1fr;
    gap: 30px;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2.5rem;
  }
  
  .section-title {
    font-size: 2.2rem;
  }
  
  .contact-form {
    padding: 30px;
  }
  
  .hero-stats {
    flex-direction: column;
    gap: 20px;
  }
}

/* Video Story Modal */
.video-modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(26, 35, 50, 0.95);
  backdrop-filter: blur(15px);
  z-index: 3000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.video-modal {
  background: white;
  border-radius: 25px;
  max-width: 900px;
  width: 100%;
  max-height: 90vh;
  overflow: hidden;
  position: relative;
  box-shadow: var(--shadow-strong);
  animation: videoModalSlideIn 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes videoModalSlideIn {
  from {
    opacity: 0;
    transform: scale(0.8) translateY(30px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.video-modal-close {
  position: absolute;
  top: 15px;
  right: 15px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  z-index: 10;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.video-modal-close:hover {
  background: var(--primary-gold);
  transform: scale(1.1);
}

.video-container {
  width: 100%;
  height: 500px;
  position: relative;
  background: #000;
  border-radius: 25px 25px 0 0;
}

.video-container iframe {
  border-radius: 25px 25px 0 0;
}

.video-info {
  padding: 30px;
  text-align: center;
}

.video-info h3 {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--primary-navy);
  margin-bottom: 15px;
}

.video-info p {
  color: var(--secondary-charcoal);
  line-height: 1.6;
  font-size: 1.1rem;
}

@media (max-width: 768px) {
  .video-modal {
    margin: 10px;
    max-height: 95vh;
  }
  
  .video-container {
    height: 250px;
  }
  
  .video-info {
    padding: 20px;
  }
  
  .video-info h3 {
    font-size: 1.4rem;
  }
  
  .video-info p {
    font-size: 1rem;
  }
}

/* Cart Styles */
.nav-cart {
  position: relative;
}

.cart-btn {
  background: none;
  border: none;
  color: white;
  font-size: 1.2rem;
  cursor: pointer;
  position: relative;
  padding: 0.5rem;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.cart-btn:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: scale(1.1);
}

.cart-icon {
  font-size: 1.5rem;
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: #ff6b6b;
  color: white;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  font-size: 0.8rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.cart-dropdown {
  position: absolute;
  top: 100%;
  right: 0;
  background: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  width: 350px;
  max-height: 500px;
  overflow-y: auto;
  z-index: 1000;
  animation: slideDown 0.3s ease;
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
  padding: 1rem;
  border-bottom: 1px solid #eee;
}

.cart-header h3 {
  margin: 0;
  color: #333;
  font-size: 1.2rem;
}

.close-cart {
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
}

.close-cart:hover {
  background: #f5f5f5;
  color: #333;
}

.cart-items {
  padding: 1rem;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #eee;
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
  margin: 0 0 0.25rem 0;
  font-size: 0.9rem;
  color: #333;
}

.cart-item-price {
  margin: 0 0 0.5rem 0;
  font-weight: bold;
  color: #2c5aa0;
}

.quantity-controls {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.quantity-controls button {
  background: #f0f0f0;
  border: none;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.quantity-controls button:hover {
  background: #e0e0e0;
}

.quantity-controls span {
  min-width: 20px;
  text-align: center;
  font-weight: bold;
}

.remove-item {
  background: #ff6b6b;
  border: none;
  color: white;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
}

.remove-item:hover {
  background: #ff5252;
}

.cart-empty {
  padding: 2rem;
  text-align: center;
  color: #666;
}

.cart-footer {
  padding: 1rem;
  border-top: 1px solid #eee;
  background: #f9f9f9;
  border-radius: 0 0 12px 12px;
}

.cart-total {
  margin-bottom: 1rem;
  text-align: center;
  font-size: 1.1rem;
  color: #333;
}

.checkout-btn {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 0.75rem;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
}

.checkout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.btn-add-to-cart {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 0.75rem 1rem;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 1rem;
}

.btn-add-to-cart:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Close dropdown when clicking outside */
@media (max-width: 768px) {
  .cart-dropdown {
    width: 300px;
    right: -50px;
  }
}

/* Contact Us Button Styles */
.btn-contact {
  background: linear-gradient(135deg, var(--primary-gold), #b8941f);
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-left: 1rem;
}

.btn-contact:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(212, 175, 55, 0.4);
}

.btn-contact .contact-icon {
  font-size: 1.2rem;
  transition: transform 0.3s ease;
}

.btn-contact:hover .contact-icon {
  transform: scale(1.2);
}

/* Contact Form Modal Styles */
.contact-form-modal {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  max-width: 600px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  animation: modalSlideIn 0.3s ease-out;
}

@keyframes modalSlideIn {
  from {
    opacity: 0;
    transform: translateY(-50px) scale(0.9);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.contact-form-content {
  width: 100%;
}

.contact-title {
  font-size: 2rem;
  font-weight: 700;
  color: var(--primary-navy);
  margin-bottom: 0.5rem;
  text-align: center;
}

.contact-subtitle {
  color: var(--text-secondary);
  text-align: center;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-weight: 600;
  color: var(--primary-navy);
  font-size: 0.95rem;
}

.form-group input,
.form-group select,
.form-group textarea {
  padding: 1rem;
  border: 2px solid #e1e5e9;
  border-radius: 12px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: #fafbfc;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary-gold);
  background: white;
  box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
}

.form-group input.error,
.form-group select.error,
.form-group textarea.error {
  border-color: #e74c3c;
  background: #fdf2f2;
}

.error-message {
  color: #e74c3c;
  font-size: 0.85rem;
  font-weight: 500;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
  font-family: inherit;
}

.form-group select {
  cursor: pointer;
}

.form-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
  margin-top: 1rem;
}

.btn-cancel {
  background: #f8f9fa;
  color: var(--text-secondary);
  border: 2px solid #e9ecef;
  padding: 0.75rem 1.5rem;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-cancel:hover {
  background: #e9ecef;
  color: var(--primary-navy);
}

.btn-submit {
  background: linear-gradient(135deg, var(--primary-gold), #b8941f);
  color: white;
  border: none;
  padding: 0.75rem 2rem;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.btn-submit:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(212, 175, 55, 0.4);
}

.btn-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

/* Responsive Design for Contact Form */
@media (max-width: 768px) {
  .contact-form-modal {
    padding: 1.5rem;
    margin: 1rem;
    max-width: calc(100% - 2rem);
  }
  
  .contact-title {
    font-size: 1.5rem;
  }
  
  .form-actions {
    flex-direction: column;
  }
  
  .btn-contact {
    margin-left: 0;
    margin-top: 0.5rem;
    padding: 0.8rem 1.5rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .hero-buttons {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }
  
  .btn-contact {
    margin-left: 0;
    width: 100%;
    justify-content: center;
  }
}
</style>
