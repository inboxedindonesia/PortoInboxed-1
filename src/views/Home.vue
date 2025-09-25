<template>
  <div id="app">
    <!-- Promo Bar Section -->
    <div class="promo-bar" v-if="showPromo">
      <div class="promo-content">
        <div class="promo-text">
          <span class="promo-icon">🎉</span>
          <span class="promo-message">{{ currentPromo.message }}</span>
        </div>
        <button class="promo-close" @click="closePromo">×</button>
      </div>
    </div>

    <!-- Header Component -->
    <Header ref="header" />

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-background-elements">
        <div class="floating-element element-1"></div>
        <div class="floating-element element-2"></div>
        <div class="floating-element element-3"></div>
        <div class="floating-element element-4"></div>
      </div>
      
      <div class="hero-content">
        <div class="hero-text">
          <h1 class="hero-title">
            <span class="title-line-1">Transform Your</span>
            <span class="title-line-2">Living Space</span>
            <span class="title-accent">Into Art</span>
          </h1>
          <p class="hero-subtitle">
            Discover our curated collection of premium furniture that seamlessly blends 
            <span class="highlight">elegance</span>, <span class="highlight">comfort</span>, 
            and <span class="highlight">functionality</span> to create spaces that inspire.
          </p>
          <div class="hero-stats">
            <div class="stat-item">
              <div class="stat-number">10K+</div>
              <div class="stat-label">Happy Customers</div>
            </div>
            <div class="stat-divider"></div>
            <div class="stat-item">
              <div class="stat-number">500+</div>
              <div class="stat-label">Premium Designs</div>
            </div>
            <div class="stat-divider"></div>
            <div class="stat-item">
              <div class="stat-number">35+</div>
              <div class="stat-label">Years Experience</div>
            </div>
          </div>
          <div class="hero-buttons">
            <router-link to="/catalog" class="btn btn-primary">
              <span class="btn-text">Explore Collection</span>
              <span class="btn-icon">→</span>
            </router-link>
            <button class="btn btn-secondary" @click="showVideoModal = true">
              <span class="btn-icon">▶</span>
              <span class="btn-text">Watch Our Story</span>
            </button>
          </div>
        </div>
        <div class="hero-visual">
          <div class="hero-image-container">
            <div class="image-frame">
              <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=800&h=600&fit=crop" alt="Luxury Furniture" class="hero-image">
            </div>
            
            <div class="image-overlay-elements">
              <!-- Premium Badge moved back to image overlay -->
              <div class="premium-badge-overlay">
                <div class="badge-text">Premium Furniture Collection</div>
              </div>
              <div class="overlay-card card-1">
                <div class="card-text">Award Winning Design</div>
              </div>
              <div class="overlay-card card-2">
                <div class="card-text">5-Star Rating</div>
              </div>
              <div class="overlay-card card-3">
                <div class="card-text">Free Delivery</div>
              </div>
            </div>
          </div>
          
          <!-- Small Images as Card Boxes -->
          <div class="image-cards-container">
            <div class="image-card">
              <img src="https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=300&h=200&fit=crop" alt="Modern Sofa" class="card-img">
              <div class="card-overlay">
                <span class="card-title">Modern Sofa</span>
              </div>
            </div>
            <div class="image-card">
              <img src="https://images.unsplash.com/photo-1567538096630-e0c55bd6374c?w=300&h=200&fit=crop" alt="Elegant Chair" class="card-img">
              <div class="card-overlay">
                <span class="card-title">Elegant Chair</span>
              </div>
            </div>
            <div class="image-card">
              <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=300&h=200&fit=crop" alt="Dining Table" class="card-img">
              <div class="card-overlay">
                <span class="card-title">Dining Table</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>



    <!-- Our Clients Section -->
    <section class="clients-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Trusted by Leading Brands</h2>
          <p class="section-subtitle">Join thousands of satisfied customers who trust LuxeFurniture</p>
        </div>
        
        <div class="clients-marquee">
          <div class="marquee-track">
            <div class="client-logo">
              <!-- Modern Furniture Brand 1 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(30, 20)">
                  <rect x="10" y="10" width="70" height="40" rx="8" fill="none" stroke="#2c3e50" stroke-width="3"/>
                  <rect x="20" y="20" width="15" height="20" rx="2" fill="#3498db"/>
                  <rect x="40" y="15" width="15" height="25" rx="2" fill="#e74c3c"/>
                  <rect x="60" y="18" width="15" height="22" rx="2" fill="#f39c12"/>
                  <text x="45" y="55" text-anchor="middle" fill="#2c3e50" font-family="Arial, sans-serif" font-size="10" font-weight="bold">LUXE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 2 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(40, 25)">
                  <circle cx="35" cy="15" r="12" fill="none" stroke="#8e44ad" stroke-width="3"/>
                  <path d="M25 15 L35 5 L45 15 L35 25 Z" fill="#9b59b6"/>
                  <text x="35" y="35" text-anchor="middle" fill="#8e44ad" font-family="Arial, sans-serif" font-size="12" font-weight="bold">ELITE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 3 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(35, 20)">
                  <path d="M40 10 L60 10 L70 30 L50 40 L30 30 L40 10 Z" fill="#27ae60" opacity="0.8"/>
                  <path d="M40 15 L55 15 L60 25 L50 30 L35 25 L40 15 Z" fill="#2ecc71"/>
                  <text x="50" y="50" text-anchor="middle" fill="#27ae60" font-family="Arial, sans-serif" font-size="11" font-weight="bold">VERDE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 4 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(45, 25)">
                  <rect x="0" y="0" width="60" height="8" rx="4" fill="#e67e22"/>
                  <rect x="10" y="12" width="40" height="8" rx="4" fill="#d35400"/>
                  <rect x="20" y="24" width="20" height="8" rx="4" fill="#e67e22"/>
                  <text x="30" y="45" text-anchor="middle" fill="#d35400" font-family="Arial, sans-serif" font-size="10" font-weight="bold">TIMBER</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 5 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(50, 20)">
                  <ellipse cx="25" cy="20" rx="20" ry="15" fill="none" stroke="#34495e" stroke-width="2"/>
                  <ellipse cx="25" cy="20" rx="12" ry="8" fill="#95a5a6"/>
                  <text x="25" y="45" text-anchor="middle" fill="#34495e" font-family="Arial, sans-serif" font-size="11" font-weight="bold">NOVA</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 6 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(40, 22)">
                  <polygon points="35,8 45,18 35,28 25,18" fill="#16a085"/>
                  <polygon points="35,12 41,18 35,24 29,18" fill="#1abc9c"/>
                  <text x="35" y="42" text-anchor="middle" fill="#16a085" font-family="Arial, sans-serif" font-size="10" font-weight="bold">CRYSTAL</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 7 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(45, 25)">
                  <path d="M30 5 L40 15 L30 25 L20 15 Z" fill="#c0392b"/>
                  <path d="M30 10 L35 15 L30 20 L25 15 Z" fill="#e74c3c"/>
                  <text x="30" y="38" text-anchor="middle" fill="#c0392b" font-family="Arial, sans-serif" font-size="10" font-weight="bold">RUBY</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 8 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(42, 20)">
                  <rect x="15" y="10" width="36" height="20" rx="10" fill="none" stroke="#7f8c8d" stroke-width="2"/>
                  <circle cx="33" cy="20" r="6" fill="#bdc3c7"/>
                  <text x="33" y="42" text-anchor="middle" fill="#7f8c8d" font-family="Arial, sans-serif" font-size="10" font-weight="bold">STEEL</text>
                </g>
              </svg>
            </div>
            <!-- Duplicate for seamless loop -->
            <div class="client-logo">
              <!-- Modern Furniture Brand 1 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(30, 20)">
                  <rect x="10" y="10" width="70" height="40" rx="8" fill="none" stroke="#2c3e50" stroke-width="3"/>
                  <rect x="20" y="20" width="15" height="20" rx="2" fill="#3498db"/>
                  <rect x="40" y="15" width="15" height="25" rx="2" fill="#e74c3c"/>
                  <rect x="60" y="18" width="15" height="22" rx="2" fill="#f39c12"/>
                  <text x="45" y="55" text-anchor="middle" fill="#2c3e50" font-family="Arial, sans-serif" font-size="10" font-weight="bold">LUXE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 2 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(40, 25)">
                  <circle cx="35" cy="15" r="12" fill="none" stroke="#8e44ad" stroke-width="3"/>
                  <path d="M25 15 L35 5 L45 15 L35 25 Z" fill="#9b59b6"/>
                  <text x="35" y="35" text-anchor="middle" fill="#8e44ad" font-family="Arial, sans-serif" font-size="12" font-weight="bold">ELITE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 3 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(35, 20)">
                  <path d="M40 10 L60 10 L70 30 L50 40 L30 30 L40 10 Z" fill="#27ae60" opacity="0.8"/>
                  <path d="M40 15 L55 15 L60 25 L50 30 L35 25 L40 15 Z" fill="#2ecc71"/>
                  <text x="50" y="50" text-anchor="middle" fill="#27ae60" font-family="Arial, sans-serif" font-size="11" font-weight="bold">VERDE</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 4 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(45, 25)">
                  <rect x="0" y="0" width="60" height="8" rx="4" fill="#e67e22"/>
                  <rect x="10" y="12" width="40" height="8" rx="4" fill="#d35400"/>
                  <rect x="20" y="24" width="20" height="8" rx="4" fill="#e67e22"/>
                  <text x="30" y="45" text-anchor="middle" fill="#d35400" font-family="Arial, sans-serif" font-size="10" font-weight="bold">TIMBER</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 5 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(50, 20)">
                  <ellipse cx="25" cy="20" rx="20" ry="15" fill="none" stroke="#34495e" stroke-width="2"/>
                  <ellipse cx="25" cy="20" rx="12" ry="8" fill="#95a5a6"/>
                  <text x="25" y="45" text-anchor="middle" fill="#34495e" font-family="Arial, sans-serif" font-size="11" font-weight="bold">NOVA</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 6 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(40, 22)">
                  <polygon points="35,8 45,18 35,28 25,18" fill="#16a085"/>
                  <polygon points="35,12 41,18 35,24 29,18" fill="#1abc9c"/>
                  <text x="35" y="42" text-anchor="middle" fill="#16a085" font-family="Arial, sans-serif" font-size="10" font-weight="bold">CRYSTAL</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 7 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(45, 25)">
                  <path d="M30 5 L40 15 L30 25 L20 15 Z" fill="#c0392b"/>
                  <path d="M30 10 L35 15 L30 20 L25 15 Z" fill="#e74c3c"/>
                  <text x="30" y="38" text-anchor="middle" fill="#c0392b" font-family="Arial, sans-serif" font-size="10" font-weight="bold">RUBY</text>
                </g>
              </svg>
            </div>
            <div class="client-logo">
              <!-- Modern Furniture Brand 8 -->
              <svg width="150" height="80" viewBox="0 0 150 80" xmlns="http://www.w3.org/2000/svg">
                <g transform="translate(42, 20)">
                  <rect x="15" y="10" width="36" height="20" rx="10" fill="none" stroke="#7f8c8d" stroke-width="2"/>
                  <circle cx="33" cy="20" r="6" fill="#bdc3c7"/>
                  <text x="33" y="42" text-anchor="middle" fill="#7f8c8d" font-family="Arial, sans-serif" font-size="10" font-weight="bold">STEEL</text>
                </g>
              </svg>
            </div>
          </div>
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
          
          <!-- Navigation Buttons - REMOVED -->
          
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
                <button class="btn-quick-view" @click.stop="openQuickView(product)">Quick View</button>
                <button class="btn-wishlist" @click.stop="addToWishlist(product)">
                  <span class="heart-icon">♡</span>
                  <span class="wishlist-text">Love</span>
                </button>
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
                <h3>10K+</h3>
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
          <p class="section-subtitle">Complete solutions for your dream furniture needs</p>
        </div>
        
        <div class="services-grid">
          <div class="service-card premium">
            <div class="service-number">01</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=400&h=200&fit=crop&crop=center" alt="Interior Design Consultation" class="service-image">
            </div>
            <div class="service-content">
              <h3>Interior Design Consultation</h3>
              <p>Complete interior design consultation with 3D visualization and space optimization to create your dream living space</p>
              <div class="service-features">
                <span class="feature-tag">3D Visualization</span>
                <span class="feature-tag">Space Planning</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Interior Design Consultation')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
          </div>

          <div class="service-card premium">
            <div class="service-number">02</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1581539250439-c96689b516dd?w=400&h=200&fit=crop&crop=center" alt="Installation & Assembly" class="service-image">
            </div>
            <div class="service-content">
              <h3>Installation & Assembly</h3>
              <p>Professional furniture installation and assembly services with quality guarantee and customer satisfaction</p>
              <div class="service-features">
                <span class="feature-tag">Professional Team</span>
                <span class="feature-tag">Quality Guarantee</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Installation & Assembly')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
          </div>

          <div class="service-card premium">
            <div class="service-number">03</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=400&h=200&fit=crop&crop=center" alt="Maintenance & Care" class="service-image">
            </div>
            <div class="service-content">
              <h3>Maintenance & Care</h3>
              <p>Regular maintenance services to keep your furniture in perfect condition and ensure long-lasting durability</p>
              <div class="service-features">
                <span class="feature-tag">Regular Care</span>
                <span class="feature-tag">Long Lasting</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Maintenance & Care')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
          </div>

          <div class="service-card premium">
            <div class="service-number">04</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=400&h=200&fit=crop&crop=center" alt="Custom Furniture" class="service-image">
            </div>
            <div class="service-content">
              <h3>Custom Furniture</h3>
              <p>Bespoke furniture designed and crafted specifically according to your unique specifications and requirements</p>
              <div class="service-features">
                <span class="feature-tag">Bespoke Design</span>
                <span class="feature-tag">Premium Materials</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Custom Furniture')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
          </div>

          <div class="service-card premium">
            <div class="service-number">05</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1560472354-b33ff0c44a43?w=400&h=200&fit=crop&crop=center" alt="Space Planning" class="service-image">
            </div>
            <div class="service-content">
              <h3>Space Planning</h3>
              <p>Space layout optimization to maximize functionality and aesthetics with modern design approaches</p>
              <div class="service-features">
                <span class="feature-tag">Space Optimization</span>
                <span class="feature-tag">Modern Design</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Space Planning')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
          </div>

          <div class="service-card premium">
            <div class="service-number">06</div>
            <div class="service-visual">
              <img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=400&h=200&fit=crop&crop=center" alt="Relocation Services" class="service-image">
            </div>
            <div class="service-content">
              <h3>Relocation Services</h3>
              <p>Complete furniture moving and arrangement services for your new space with safe handling procedures</p>
              <div class="service-features">
                <span class="feature-tag">Safe Handling</span>
                <span class="feature-tag">Complete Setup</span>
              </div>
              <button class="inquiry-btn" @click="openInquiry('Relocation Services')">
                <span>Inquiry Now</span>
                <i class="fas fa-arrow-right"></i>
              </button>
            </div>
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
              <div class="form-buttons">
                <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
                  <span v-if="isSubmitting">Sending...</span>
                  <span v-else">Send Message</span>
                </button>
                <button type="button" class="btn btn-whatsapp" @click="callWhatsApp">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.488"/>
                  </svg>
                  Call Us Now
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer Component -->
    <Footer />

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

    <!-- Product Detail Modal -->
    <div v-if="showProductDetail" class="modal-overlay" @click="closeProductDetail">
      <div class="product-detail-modal" @click.stop>
        <button class="modal-close" @click="closeProductDetail">×</button>
        <div class="product-detail-content">
          <div class="product-gallery">
            <div class="main-image">
              <img :src="selectedSlideProduct.image" :alt="selectedSlideProduct.title" />
            </div>
            <div class="thumbnail-gallery">
              <img 
                v-for="(img, index) in selectedSlideProduct.gallery" 
                :key="index" 
                :src="img" 
                :alt="`${selectedSlideProduct.title} ${index + 1}`"
                class="thumbnail"
              />
            </div>
          </div>
          <div class="product-info">
            <h2>{{ selectedSlideProduct.title }}</h2>
            <p class="product-description">{{ selectedSlideProduct.description }}</p>
            <div class="price-section">
              <span class="current-price">${{ selectedSlideProduct.price?.toLocaleString() }}</span>
            </div>
            
            <div class="features-section">
              <h3>Fitur Unggulan</h3>
              <ul class="features-list">
                <li v-for="feature in selectedSlideProduct.features" :key="feature">
                  <i class="feature-icon">✓</i>
                  {{ feature }}
                </li>
              </ul>
            </div>
            
            <div class="specifications-section">
              <h3>Spesifikasi</h3>
              <div class="spec-grid">
                <div 
                  v-for="(value, key) in selectedSlideProduct.specifications" 
                  :key="key" 
                  class="spec-item"
                >
                  <span class="spec-label">{{ key }}:</span>
                  <span class="spec-value">{{ value }}</span>
                </div>
              </div>
            </div>
            
            <div class="action-buttons">
              <button class="btn btn-primary add-to-cart-btn" @click="addSlideProductToCart(selectedSlideProduct)">
                <i class="cart-icon">🛒</i>
                Tambah ke Keranjang
              </button>
              <button class="btn btn-secondary wishlist-btn" @click="addToWishlist(selectedSlideProduct)">
                <i class="heart-icon">♡</i>
                Tambah ke Wishlist
              </button>
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
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'Home',
  components: {
    Header,
    Footer
  },
  setup() {
    const isScrolled = ref(false)
    const showQuickView = ref(false)
    const selectedProduct = ref({})
    const wishlist = ref([])
    const showVideoModal = ref(false)
    const cart = ref([])
    const showCartDropdown = ref(false)
    const isSubmitting = ref(false)
    
    // Promo bar states
    const showPromo = ref(true)
    const currentPromoIndex = ref(0)
    const promoMessages = ref([
      { message: "🎉 Free Delivery on Orders Over $500! Limited Time Offer" },
      { message: "✨ New Collection: 30% Off Premium Furniture" },
      { message: "🚚 Same Day Delivery Available in Selected Areas" }
    ])
    
    const currentPromo = computed(() => promoMessages.value[currentPromoIndex.value])
    
    // Product detail popup states
    const showProductDetail = ref(false)
    const selectedSlideProduct = ref({})
    
    // Slider data and state
    const currentSlide = ref(0)
    const furnitureSlides = ref([
      {
        id: 1,
        title: "Luxury Living Room Collection",
        description: "Transform your living space with our premium sofa sets, coffee tables, and entertainment units crafted from the finest materials.",
        price: 4299,
        image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=800&h=500&fit=crop",
        features: ['Premium Italian Leather', 'Free Delivery & Installation', '2 Year Warranty', 'Expert Assembly Service'],
        specifications: {
          'Material': 'Premium Italian Leather & Hardwood Frame',
          'Dimensions': '220cm x 95cm x 85cm',
          'Weight': '65kg',
          'Color Options': 'Brown, Black, Cream, Navy',
          'Assembly': 'Professional Installation Included',
          'Warranty': '2 Years Full Coverage'
        },
        gallery: [
          "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 2,
        title: "Modern Dining Experience",
        description: "Elegant dining sets that bring family and friends together for memorable meals with contemporary design and comfort.",
        price: 3199,
        image: "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=800&h=500&fit=crop",
        features: ['Solid Oak Wood', 'Seats 6-8 People', '2 Year Warranty', 'Scratch Resistant Finish'],
        specifications: {
          'Material': 'Solid Oak Wood with Protective Finish',
          'Dimensions': '180cm x 90cm x 75cm',
          'Weight': '55kg',
          'Seating Capacity': '6-8 People',
          'Assembly': 'Easy Assembly with Instructions',
          'Warranty': '2 Years Manufacturing Defects'
        },
        gallery: [
          "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 3,
        title: "Bedroom Sanctuary",
        description: "Create your perfect retreat with our luxurious bedroom furniture collections designed for ultimate comfort and style.",
        price: 5499,
        image: "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=800&h=500&fit=crop",
        features: ['King Size Bed Frame', 'Built-in Storage', '2 Year Warranty', 'Premium Mattress Compatible'],
        specifications: {
          'Material': 'Engineered Wood with Veneer Finish',
          'Dimensions': '210cm x 180cm x 120cm',
          'Weight': '75kg',
          'Bed Size': 'King Size (180cm x 200cm)',
          'Storage': 'Built-in Drawers and Compartments',
          'Warranty': '2 Years Structural Warranty'
        },
        gallery: [
          "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 4,
        title: "Executive Office Suite",
        description: "Professional workspace furniture designed for productivity and comfort with ergonomic features and modern aesthetics.",
        price: 2899,
        image: "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=800&h=500&fit=crop",
        features: ['Ergonomic Design', 'Height Adjustable', '2 Year Warranty', 'Cable Management System'],
        specifications: {
          'Material': 'Steel Frame with Laminated Wood Top',
          'Dimensions': '160cm x 80cm x 75cm',
          'Weight': '45kg',
          'Height Range': '70cm - 80cm (Adjustable)',
          'Features': 'Built-in Cable Management',
          'Warranty': '2 Years Office Use Warranty'
        },
        gallery: [
          "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 5,
        title: "Outdoor Paradise",
        description: "Weather-resistant outdoor furniture for your patio, garden, or balcony designed to withstand all seasons.",
        price: 1899,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=800&h=500&fit=crop",
        features: ['Weather Resistant', 'UV Protection', '3 Year Warranty', 'Easy Maintenance'],
        specifications: {
          'Material': 'Aluminum Frame with Weather-Resistant Fabric',
          'Dimensions': '200cm x 100cm x 85cm',
          'Weight': '25kg',
          'Weather Rating': 'All-Season Outdoor Use',
          'Maintenance': 'Easy Clean with Water',
          'Warranty': '3 Years Weather Resistance'
        },
        gallery: [
          "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 6,
        title: "Kids Wonderland Collection",
        description: "Safe, colorful, and fun furniture designed specifically for children's rooms and play areas with rounded edges and non-toxic materials.",
        price: 2299,
        image: "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&h=500&fit=crop",
        features: ['Child Safe Materials', 'Rounded Edges', '2 Year Warranty', 'Easy Assembly'],
        specifications: {
          'Material': 'Non-Toxic MDF with Child-Safe Paint',
          'Dimensions': '150cm x 80cm x 120cm',
          'Weight': '35kg',
          'Age Range': '3-12 Years',
          'Safety': 'Rounded Edges & Non-Toxic Materials',
          'Warranty': '2 Years Child Safety Warranty'
        },
        gallery: [
          "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1541558869434-2840d308329a?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=600&h=400&fit=crop"
        ]
      },
      {
        id: 7,
        title: "Vintage Classic Series",
        description: "Timeless vintage-inspired furniture that adds character and elegance to any space with handcrafted details and premium finishes.",
        price: 3799,
        image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=800&h=500&fit=crop",
        features: ['Handcrafted Details', 'Vintage Finish', '2 Year Warranty', 'Unique Design'],
        specifications: {
          'Material': 'Reclaimed Wood with Vintage Finish',
          'Dimensions': '190cm x 85cm x 90cm',
          'Weight': '50kg',
          'Style': 'Vintage/Antique Inspired',
          'Finish': 'Hand-Applied Distressed Finish',
          'Warranty': '2 Years Craftsmanship Warranty'
        },
        gallery: [
          "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=800&h=500&fit=crop",
          "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=600&h=400&fit=crop",
          "https://images.unsplash.com/photo-1449247709967-d4461a6a6103?w=600&h=400&fit=crop"
        ]
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
      },
      {
        id: 5,
        name: "Luxe Coffee Table Set",
        price: 1299,
        rating: 5,
        reviews: 94,
        image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=400&h=300&fit=crop",
        description: "Modern glass-top coffee table with matching side tables"
      },
      {
        id: 6,
        name: "Comfort Recliner Chair",
        price: 899,
        rating: 4,
        reviews: 167,
        image: "https://images.unsplash.com/photo-1506439773649-6e0eb8cfb237?w=400&h=300&fit=crop",
        description: "Premium leather recliner with massage and heating features"
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

    const closeProductDetail = () => {
      showProductDetail.value = false
      selectedSlideProduct.value = {}
    }

    const addSlideProductToCart = (product) => {
      const existingItem = cart.value.find(item => item.id === product.id)
      
      if (existingItem) {
        existingItem.quantity += 1
      } else {
        cart.value.push({
          id: product.id,
          name: product.title,
          price: product.price,
          image: product.image,
          quantity: 1
        })
      }
      
      alert(`${product.title} berhasil ditambahkan ke keranjang!`)
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

    const increaseQuantity = (productId) => {
      const item = cart.value.find(item => item.id === productId)
      if (item) {
        item.quantity += 1
      }
    }

    const decreaseQuantity = (productId) => {
      const item = cart.value.find(item => item.id === productId)
      if (item && item.quantity > 1) {
        item.quantity -= 1
      }
    }

    const viewFullCart = () => {
      showCartDropdown.value = false
      alert('Fitur halaman keranjang lengkap akan segera hadir!')
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
      // Set selected product and show popup with complete data
      selectedSlideProduct.value = slide
      showProductDetail.value = true
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

    // Inquiry function for services
    const openInquiry = (serviceName) => {
      const message = `Hello! I'm interested in learning more about your ${serviceName} service. Could you please provide more details about pricing, timeline, and what's included?`
      
      // Create WhatsApp link with pre-filled message
      const phoneNumber = '+1234567890' // Replace with actual business phone number
      const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`
      
      // Open WhatsApp in new tab
      window.open(whatsappUrl, '_blank')
    }

    const callAgent = (agentType) => {
      const agents = {
        design: {
          name: 'Sarah Johnson',
          phone: '6281234567890',
          message: 'Hi Sarah! I need help with interior design and custom furniture consultation. Can you assist me with space planning and design ideas?'
        },
        sales: {
          name: 'Michael Chen', 
          phone: '6281234567891',
          message: 'Hi Michael! I\'m interested in your furniture collection and would like to know about pricing, discounts, and bulk order options.'
        },
        support: {
          name: 'Emma Rodriguez',
          phone: '6281234567892', 
          message: 'Hi Emma! I need assistance with my order, delivery information, or have some general questions about your services.'
        }
      }

      const agent = agents[agentType]
      if (agent) {
        const whatsappUrl = `https://wa.me/${agent.phone}?text=${encodeURIComponent(agent.message)}`
        window.open(whatsappUrl, '_blank')
      }
    }

    const callWhatsApp = () => {
      const message = `Hello! I'm interested in your furniture collection and would like to get more information about your products and services.`
      const phoneNumber = '6281234567890' // Replace with actual business phone number
      const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`
      window.open(whatsappUrl, '_blank')
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
      // Product detail popup
      showProductDetail,
      selectedSlideProduct,
      closeProductDetail,
      addSlideProductToCart,
      increaseQuantity,
      decreaseQuantity,
      viewFullCart,
      // Slider variables and methods
      currentSlide,
      furnitureSlides,
      nextSlide,
      prevSlide,
      goToSlide,
      viewProduct,
      // Services inquiry
      openInquiry,
      // WhatsApp agents
      callAgent,
      callWhatsApp,
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
  padding: 20px;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 15px 0;
  border-bottom: 1px solid rgba(226, 232, 240, 0.3);
  transition: all 0.3s ease;
}

.cart-item:hover {
  background: rgba(102, 126, 234, 0.02);
  border-radius: 12px;
  padding: 15px 12px;
  margin: 0 -12px;
}

.cart-item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 12px;
  transition: all 0.3s ease;
}

.cart-item:hover .cart-item-image {
  transform: scale(1.05);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.cart-item-info {
  flex: 1;
}

.cart-item-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.cart-item-info h4 {
  font-size: 0.925rem;
  margin-bottom: 0;
  color: #334155;
  font-weight: 600;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.2px;
  line-height: 1.3;
}

.item-price {
  color: #667eea;
  font-size: 0.875rem;
  font-weight: 600;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.quantity-controls {
  display: flex;
  align-items: center;
  gap: 8px;
}

.qty-btn {
  background: #f1f5f9;
  border: 1px solid #e2e8f0;
  color: #475569;
  width: 28px;
  height: 28px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 600;
  transition: all 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.qty-btn:hover {
  background: #e2e8f0;
  border-color: #cbd5e1;
}

.quantity {
  font-size: 0.875rem;
  font-weight: 600;
  color: #334155;
  min-width: 20px;
  text-align: center;
}

.item-total {
  color: #059669;
  font-size: 0.875rem;
  font-weight: 700;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.cart-item-info p {
  color: #64748b;
  font-size: 0.825rem;
  font-weight: 500;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.4;
}

.remove-btn {
  background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
  color: white;
  border: none;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
}

.remove-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 12px rgba(255, 107, 107, 0.3);
}

.cart-summary {
  border-top: 2px solid rgba(102, 126, 234, 0.1);
  margin-top: 15px;
  padding-top: 18px;
}

.cart-total {
  text-align: center;
  padding-bottom: 15px;
  color: #334155;
  font-weight: 700;
  font-size: 1.05rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -0.3px;
}

.cart-actions {
  display: flex;
  gap: 10px;
}

.view-cart-btn {
  flex: 1;
  background: #f8fafc;
  color: #475569;
  border: 2px solid #e2e8f0;
  padding: 12px 16px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  font-size: 0.875rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.view-cart-btn:hover {
  background: #e2e8f0;
  border-color: #cbd5e1;
}

.checkout-btn {
  flex: 1;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 12px 16px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  font-size: 0.875rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 16px rgba(102, 126, 234, 0.3);
}

.checkout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
}

.empty-cart {
  padding: 40px 20px;
  text-align: center;
  color: #64748b;
  font-weight: 500;
}

.empty-cart-icon {
  font-size: 3rem;
  margin-bottom: 15px;
  opacity: 0.6;
}

.continue-shopping-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  margin-top: 15px;
  font-size: 0.875rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.continue-shopping-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
}

/* Hero Section */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: linear-gradient(135deg, #0f0c29 0%, #24243e 35%, #302b63 70%, #0f0c29 100%);
  color: white;
  padding-top: 80px;
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 30%, rgba(102, 126, 234, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(240, 147, 251, 0.2) 0%, transparent 50%),
    radial-gradient(circle at 40% 80%, rgba(118, 75, 162, 0.25) 0%, transparent 50%);
  z-index: 1;
}

.hero-background-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.floating-element {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
  backdrop-filter: blur(10px);
  animation: float 6s ease-in-out infinite;
}

.element-1 {
  width: 120px;
  height: 120px;
  top: 15%;
  left: 10%;
  animation-delay: 0s;
}

.element-2 {
  width: 80px;
  height: 80px;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
}

.element-3 {
  width: 60px;
  height: 60px;
  top: 25%;
  right: 25%;
  animation-delay: 4s;
}

.element-4 {
  width: 100px;
  height: 100px;
  bottom: 20%;
  left: 20%;
  animation-delay: 1s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: center;
  position: relative;
  z-index: 2;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.05));
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 0.8rem 1.5rem;
  border-radius: 50px;
  margin-bottom: 2rem;
  font-size: 0.9rem;
  font-weight: 500;
  animation: slideInUp 1s ease-out;
}

.badge-icon {
  font-size: 1.2rem;
  animation: sparkle 2s ease-in-out infinite;
}

@keyframes sparkle {
  0%, 100% { transform: scale(1) rotate(0deg); }
  50% { transform: scale(1.2) rotate(180deg); }
}

.hero-title {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 1.5rem;
  line-height: 1.15;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: -1.5px;
  animation: slideInUp 1s ease-out 0.2s both;
  max-width: 90%;
}

.title-line-1, .title-line-2 {
  display: block;
  background: linear-gradient(135deg, #ffffff 0%, #f8fafc 50%, #e2e8f0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.3rem;
}

.title-accent {
  display: block;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 4.2rem;
  margin-top: 0.3rem;
  text-shadow: 0 0 30px rgba(102, 126, 234, 0.5);
}

.hero-subtitle {
  font-size: 1.2rem;
  margin-bottom: 2.5rem;
  opacity: 0.9;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.85);
  font-weight: 400;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  animation: slideInUp 1s ease-out 0.4s both;
  max-width: 85%;
}

.highlight {
  background: linear-gradient(135deg, #667eea, #764ba2);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 600;
}

.hero-stats {
  display: flex;
  align-items: center;
  gap: 1.8rem;
  margin-bottom: 2.5rem;
  animation: slideInUp 1s ease-out 0.6s both;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 2rem;
  font-weight: 800;
  background: linear-gradient(135deg, #667eea, #f093fb);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  opacity: 0.7;
  font-weight: 500;
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, transparent, rgba(255, 255, 255, 0.3), transparent);
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
  animation: slideInUp 1s ease-out 0.8s both;
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.btn {
  padding: 1.2rem 2.5rem;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1.05rem;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  text-align: center;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  letter-spacing: 0.3px;
  position: relative;
  overflow: hidden;
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.btn:hover::before {
  left: 100%;
}

.btn-icon {
  font-size: 1.2rem;
  transition: transform 0.3s ease;
}

.btn:hover .btn-icon {
  transform: translateX(3px);
}

.btn-primary {
  background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
  color: #667eea;
  box-shadow: 0 8px 32px rgba(255, 255, 255, 0.3);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(255, 255, 255, 0.4);
  background: linear-gradient(135deg, #f8fafc 0%, #ffffff 100%);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.1);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(255, 255, 255, 0.2);
}

.hero-visual {
  position: relative;
  animation: slideInRight 1s ease-out 0.6s both;
}

.hero-image-container {
  position: relative;
}

.image-frame {
  position: relative;
  border-radius: 30px;
  overflow: hidden;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
  padding: 1rem;
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.hero-image {
  width: 100%;
  height: 520px;
  object-fit: cover;
  border-radius: 20px;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.hero-image:hover {
  transform: scale(1.02);
}

.image-cards-container {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
  justify-content: center;
  animation: fadeInUp 1s ease-out 1.0s both;
}

.image-card {
  position: relative;
  width: 150px;
  height: 100px;
  border-radius: 15px;
  overflow: hidden;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.image-card:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.08));
}

.card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.image-card:hover .card-img {
  transform: scale(1.05);
}

.card-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
  padding: 0.8rem 0.6rem 0.6rem;
  transform: translateY(100%);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.image-card:hover .card-overlay {
  transform: translateY(0);
}

.card-title {
  color: white;
  font-size: 0.8rem;
  font-weight: 600;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  letter-spacing: 0.3px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.additional-images {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.small-image {
  position: absolute;
  border-radius: 15px;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 0.5rem;
  animation: fadeInScale 1s ease-out both;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.small-image:hover {
  transform: scale(1.05);
  background: rgba(255, 255, 255, 0.15);
}

.small-image-1 {
  width: 120px;
  height: 80px;
  top: 10%;
  left: -8%;
  animation-delay: 0.8s;
}

.small-image-2 {
  width: 100px;
  height: 70px;
  bottom: 15%;
  left: -5%;
  animation-delay: 1.0s;
}

.small-image-3 {
  width: 110px;
  height: 75px;
  top: 60%;
  right: -8%;
  animation-delay: 1.2s;
}

.small-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.premium-badge-text {
  margin-top: 2rem;
  text-align: center;
  animation: fadeInUp 1s ease-out 1.2s both;
}

.premium-badge-text .badge-text {
  display: inline-block;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.08));
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 0.8rem 1.8rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  font-size: 0.95rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  letter-spacing: 0.5px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.premium-badge-text .badge-text:hover {
  transform: translateY(-2px) scale(1.02);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.2), rgba(255, 255, 255, 0.12));
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.premium-badge-overlay {
  position: absolute;
  top: 5%;
  left: calc(50% - 4cm);
  transform: translateX(-50%);
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(25px);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 25px;
  padding: 0.8rem 1.5rem;
  animation: fadeInScale 1s ease-out 0.8s both;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.premium-badge-overlay:hover {
  transform: translateX(-50%) translateY(-3px) scale(1.02);
  background: rgba(255, 255, 255, 0.18);
}

.premium-badge-overlay .badge-text {
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  font-size: 0.9rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  letter-spacing: 0.5px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  text-align: center;
  white-space: nowrap;
}

.image-overlay-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.overlay-card {
  position: absolute;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(30px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 25px;
  padding: 1rem 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1), 0 2px 8px rgba(255, 255, 255, 0.1) inset;
  animation: fadeInScale 1s ease-out both;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.overlay-card:hover {
  transform: translateY(-3px) scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15), 0 4px 12px rgba(255, 255, 255, 0.15) inset;
  background: rgba(255, 255, 255, 0.15);
}

.card-1 {
  top: 20%;
  right: -10%;
  animation-delay: 1.2s;
}

.card-2 {
  top: 50%;
  left: -15%;
  animation-delay: 1.4s;
}

.card-3 {
  bottom: 20%;
  right: -5%;
  animation-delay: 1.6s;
}

.card-text {
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  font-size: 1rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  letter-spacing: 0.5px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  text-align: center;
  white-space: nowrap;
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInScale {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Furniture Slider Section */
.furniture-slider-section {
  padding: 100px 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
  position: relative;
}

.furniture-slider-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 20%, rgba(102, 126, 234, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 70% 80%, rgba(118, 75, 162, 0.1) 0%, transparent 50%);
  z-index: 1;
}

.slider-container {
  position: relative;
  max-width: 1000px;
  margin: 0 auto;
  overflow: hidden;
  border-radius: 25px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.15);
  z-index: 2;
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
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 50%, #f1f3f4 100%);
  color: #2c3e50;
  position: relative;
  overflow: hidden;
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
  color: #e67e22;
  margin-bottom: 30px;
  display: block;
}

.slide-info .btn {
  align-self: flex-start;
  background: linear-gradient(135deg, #27ae60, #2ecc71);
  color: white;
  padding: 15px 30px;
  font-weight: 600;
  border-radius: 50px;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.slide-info .btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(39, 174, 96, 0.3);
  background: linear-gradient(135deg, #2ecc71, #27ae60);
  border: 2px solid rgba(39, 174, 96, 0.3);
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
  background: rgba(255, 255, 255, 0.95);
  border: 2px solid transparent;
  padding: 0.8rem 1.5rem;
  border-radius: 25px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.9rem;
  color: #333;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-wishlist .heart-icon {
  font-size: 1.1rem;
  transition: transform 0.3s ease;
}

.btn-wishlist:hover .heart-icon {
  transform: scale(1.2);
  color: #ff6b6b;
}

.btn-quick-view:hover,
.btn-wishlist:hover {
  background: #667eea;
  color: white;
  border-color: #667eea;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.3);
}

.btn-wishlist:hover {
  background: #ff6b6b;
  border-color: #ff6b6b;
  box-shadow: 0 6px 20px rgba(255, 107, 107, 0.3);
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
  padding: 120px 0;
  background: linear-gradient(135deg, #ffffff 0%, #f8fafc 50%, #f1f5f9 100%);
  position: relative;
}

.about-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 80% 30%, rgba(102, 126, 234, 0.05) 0%, transparent 60%),
              radial-gradient(circle at 20% 70%, rgba(240, 147, 251, 0.05) 0%, transparent 60%);
  z-index: 1;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: center;
  position: relative;
  z-index: 2;
}

.about-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #64748b;
  margin-bottom: 2rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.about-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2.5rem;
  margin-top: 3rem;
}

.stat {
  text-align: center;
  padding: 2rem 1.5rem;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s ease;
}

.stat:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.stat h3 {
  font-size: 2.8rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 0.5rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.stat p {
  color: #64748b;
  font-size: 1rem;
  font-weight: 500;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.about-image img {
  width: 100%;
  height: 450px;
  object-fit: cover;
  border-radius: 25px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.2);
  border: 3px solid rgba(255, 255, 255, 0.3);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.about-image img:hover {
  transform: scale(1.02) rotateY(-5deg);
  box-shadow: 0 35px 80px rgba(0, 0, 0, 0.25);
}

/* Services Section */
.services-section {
  padding: 120px 0;
  background: linear-gradient(135deg, #0f0c29 0%, #24243e 35%, #302b63 70%, #0f0c29 100%);
  position: relative;
  overflow: hidden;
}

.services-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 30%, rgba(102, 126, 234, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(240, 147, 251, 0.2) 0%, transparent 50%),
    radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.05) 0%, transparent 70%);
  z-index: 1;
}

.services-section .section-title {
  color: white;
  text-align: center;
  margin-bottom: 1rem;
  font-size: 3.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #ffffff 0%, #e2e8f0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.services-section .section-subtitle {
  color: rgba(255, 255, 255, 0.8);
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 4rem;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
  gap: 2.5rem;
  position: relative;
  z-index: 2;
}

.service-card.premium {
  background: rgba(255, 255, 255, 0.95);
  padding: 0;
  border-radius: 25px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  overflow: hidden;
  position: relative;
  min-height: 420px;
}

.service-card.premium:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 0 40px 80px rgba(0, 0, 0, 0.3);
  background: rgba(255, 255, 255, 1);
}

.service-number {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  font-weight: 700;
  color: white;
  z-index: 3;
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
}

.service-visual {
  height: 180px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  position: relative;
  overflow: hidden;
}

.visual-element {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 120px;
  height: 120px;
}

/* Design Element */
.design-shapes {
  position: relative;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
  animation: float 3s ease-in-out infinite;
}

.shape-1 {
  width: 40px;
  height: 40px;
  top: 10px;
  left: 20px;
  animation-delay: 0s;
}

.shape-2 {
  width: 60px;
  height: 60px;
  top: 30px;
  right: 10px;
  animation-delay: 1s;
}

.shape-3 {
  width: 30px;
  height: 30px;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  animation-delay: 2s;
}

/* Installation Element */
.installation-tools {
  position: relative;
  width: 100%;
  height: 100%;
}

.tool {
  position: absolute;
  background: rgba(255, 255, 255, 0.4);
  border-radius: 8px;
  animation: rotate 4s linear infinite;
}

.tool-1 {
  width: 50px;
  height: 8px;
  top: 30px;
  left: 35px;
  animation-delay: 0s;
}

.tool-2 {
  width: 8px;
  height: 50px;
  top: 35px;
  left: 56px;
  animation-delay: 1.5s;
}

.tool-3 {
  width: 35px;
  height: 35px;
  bottom: 20px;
  right: 20px;
  border-radius: 50%;
  animation-delay: 3s;
}

/* Maintenance Element */
.maintenance-circles {
  position: relative;
  width: 100%;
  height: 100%;
}

.circle {
  position: absolute;
  border: 3px solid rgba(255, 255, 255, 0.4);
  border-radius: 50%;
  animation: pulse 2s ease-in-out infinite;
}

.circle-1 {
  width: 80px;
  height: 80px;
  top: 20px;
  left: 20px;
  animation-delay: 0s;
}

.circle-2 {
  width: 60px;
  height: 60px;
  top: 30px;
  right: 15px;
  animation-delay: 0.7s;
}

.circle-3 {
  width: 40px;
  height: 40px;
  bottom: 25px;
  left: 50%;
  transform: translateX(-50%);
  animation-delay: 1.4s;
}

/* Custom Element */
.custom-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  width: 80px;
  height: 80px;
}

.grid-item {
  background: rgba(255, 255, 255, 0.4);
  border-radius: 8px;
  animation: scale 2s ease-in-out infinite;
}

.item-1 { animation-delay: 0s; }
.item-2 { animation-delay: 0.5s; }
.item-3 { animation-delay: 1s; }
.item-4 { animation-delay: 1.5s; }

/* Planning Element */
.planning-layout {
  position: relative;
  width: 100%;
  height: 100%;
}

.layout-block {
  position: absolute;
  background: rgba(255, 255, 255, 0.4);
  border-radius: 6px;
  animation: slide 3s ease-in-out infinite;
}

.block-1 {
  width: 60px;
  height: 20px;
  top: 20px;
  left: 30px;
  animation-delay: 0s;
}

.block-2 {
  width: 40px;
  height: 30px;
  top: 50px;
  left: 20px;
  animation-delay: 1s;
}

.block-3 {
  width: 50px;
  height: 25px;
  bottom: 20px;
  right: 25px;
  animation-delay: 2s;
}

/* Relocation Element */
.relocation-path {
  position: relative;
  width: 100%;
  height: 100%;
}

.path-point {
  position: absolute;
  width: 20px;
  height: 20px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 50%;
  animation: bounce 2s ease-in-out infinite;
}

.point-1 {
  top: 30px;
  left: 20px;
  animation-delay: 0s;
}

.point-2 {
  bottom: 30px;
  right: 20px;
  animation-delay: 1s;
}

.path-line {
  position: absolute;
  top: 50%;
  left: 30px;
  right: 30px;
  height: 2px;
  background: rgba(255, 255, 255, 0.4);
  transform: translateY(-50%) rotate(45deg);
  animation: glow 3s ease-in-out infinite;
}

.service-content {
  padding: 2rem;
}

.service-content h3 {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #1e293b;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.service-content p {
  color: #64748b;
  line-height: 1.7;
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

.service-features {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  margin-bottom: 1.5rem;
}

.feature-tag {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
}

.service-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 0;
  transition: transform 0.3s ease;
}

.service-card.premium:hover .service-image {
  transform: scale(1.05);
}

.inquiry-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 25px;
  font-size: 0.9rem;
  font-weight: 600;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
  width: 100%;
  justify-content: center;
}

.inquiry-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
  background: linear-gradient(135deg, #5a67d8 0%, #6b46c1 100%);
}

.inquiry-btn i {
  transition: transform 0.3s ease;
}

.inquiry-btn:hover i {
  transform: translateX(3px);
}

/* Animations */
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

@keyframes rotate {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.7; }
  50% { transform: scale(1.1); opacity: 1; }
}

@keyframes scale {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

@keyframes slide {
  0%, 100% { transform: translateX(0px); }
  50% { transform: translateX(5px); }
}

@keyframes bounce {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-8px); }
}

@keyframes glow {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 0.8; }
}

/* Contact Section */
.contact-section {
  padding: 120px 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
  position: relative;
}

.contact-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 70% 20%, rgba(102, 126, 234, 0.08) 0%, transparent 60%),
              radial-gradient(circle at 30% 80%, rgba(240, 147, 251, 0.08) 0%, transparent 60%);
  z-index: 1;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  position: relative;
  z-index: 2;
}

.contact-description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #64748b;
  margin-bottom: 3rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-bottom: 3rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 1.5rem;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 15px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s ease;
}

.contact-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
}

.contact-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  color: white;
  box-shadow: 0 8px 20px rgba(102, 126, 234, 0.3);
  margin-top: 0;
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

/* WhatsApp Agents Compact Section */
.whatsapp-agents-compact {
  margin: 30px 0;
  padding: 20px;
  background: linear-gradient(135deg, rgba(37, 211, 102, 0.1), rgba(37, 211, 102, 0.05));
  border-radius: 15px;
  border: 1px solid rgba(37, 211, 102, 0.2);
}

.agents-title-compact {
  font-size: 1.2rem;
  font-weight: 600;
  color: #25d366;
  text-align: center;
  margin-bottom: 15px;
}

.agents-logos {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.agent-logo {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: all 0.3s ease;
  min-width: 80px;
  border: 2px solid transparent;
}

.agent-logo:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(37, 211, 102, 0.3);
  border-color: #25d366;
}

.logo-icon {
  width: 40px;
  height: 40px;
  background: #25d366;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 8px;
  transition: all 0.3s ease;
}

.logo-icon svg {
  color: white;
}

.agent-logo:hover .logo-icon {
  background: #128c7e;
  transform: scale(1.1);
}

.logo-label {
  font-size: 0.85rem;
  font-weight: 600;
  color: #333;
  text-align: center;
}

.design-logo:hover {
  border-color: #e74c3c;
}

.design-logo:hover .logo-icon {
  background: #e74c3c;
}

.sales-logo:hover {
  border-color: #f39c12;
}

.sales-logo:hover .logo-icon {
  background: #f39c12;
}

.support-logo:hover {
  border-color: #3498db;
}

.support-logo:hover .logo-icon {
  background: #3498db;
}

/* WhatsApp Agents Section */
.whatsapp-agents {
  margin-top: 3rem;
  padding: 2rem;
  background: linear-gradient(135deg, #25d366 0%, #128c7e 100%);
  border-radius: 20px;
  color: white;
}

.agents-title {
  font-size: 1.8rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 0.5rem;
  color: white;
}

.agents-subtitle {
  text-align: center;
  margin-bottom: 2rem;
  opacity: 0.9;
  font-size: 1.1rem;
}

.agents-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

.agent-card {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 15px;
  padding: 1.5rem;
  color: #333;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.agent-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
}

.agent-card.premium {
  border-color: #ffd700;
  background: linear-gradient(135deg, #fff9e6 0%, #ffffff 100%);
}

.agent-card.featured {
  border-color: #ff6b6b;
  background: linear-gradient(135deg, #ffe6e6 0%, #ffffff 100%);
}

.agent-card.standard {
  border-color: #4ecdc4;
  background: linear-gradient(135deg, #e6fffe 0%, #ffffff 100%);
}

.agent-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.whatsapp-logo {
  width: 40px;
  height: 40px;
  background: #25d366;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.agent-info h4 {
  font-size: 1.2rem;
  font-weight: 700;
  margin: 0;
  color: #333;
}

.agent-role {
  font-size: 0.9rem;
  color: #666;
  font-weight: 500;
}

.online-status {
  margin-left: auto;
  font-size: 0.8rem;
}

.agent-description {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

.whatsapp-btn {
  width: 100%;
  padding: 12px 20px;
  border: none;
  border-radius: 25px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.design-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.design-btn:hover {
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
}

.sales-btn {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
}

.sales-btn:hover {
  background: linear-gradient(135deg, #f5576c 0%, #f093fb 100%);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(245, 87, 108, 0.4);
}

.support-btn {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  color: white;
}

.support-btn:hover {
  background: linear-gradient(135deg, #00f2fe 0%, #4facfe 100%);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(79, 172, 254, 0.4);
}

.btn-icon {
  font-size: 1.1rem;
}

.contact-form {
  background: rgba(255, 255, 255, 0.9);
  padding: 3rem;
  border-radius: 25px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.15);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.form-group {
  margin-bottom: 2rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.8rem;
  font-weight: 600;
  color: #374151;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1.2rem 1.5rem;
  border: 2px solid rgba(102, 126, 234, 0.2);
  border-radius: 15px;
  font-size: 1rem;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
  background: rgba(255, 255, 255, 1);
  transform: translateY(-2px);
}

.form-group textarea {
  height: 120px;
  resize: vertical;
}

.form-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.form-buttons .btn {
  flex: 1;
  min-width: 200px;
}

.btn-whatsapp {
  background: linear-gradient(135deg, #25d366 0%, #128c7e 100%);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.btn-whatsapp:hover {
  background: linear-gradient(135deg, #128c7e 0%, #25d366 100%);
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(37, 211, 102, 0.4);
}

.btn-whatsapp svg {
  transition: transform 0.3s ease;
}

.btn-whatsapp:hover svg {
  transform: scale(1.1);
}

/* Footer */
.footer {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
  color: white;
  padding: 0;
  position: relative;
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 20% 30%, rgba(102, 126, 234, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 80% 70%, rgba(118, 75, 162, 0.08) 0%, transparent 50%);
  pointer-events: none;
}

.footer-wave {
  position: relative;
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
  color: #f8fafc;
}

.footer .container {
  position: relative;
  z-index: 2;
  padding: 60px 20px 20px;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-brand {
  max-width: 400px;
}

.brand-logo {
  margin-bottom: 1.5rem;
}

.brand-logo h3 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 2.2rem;
  font-weight: 800;
  margin: 0 0 0.5rem 0;
  font-family: 'Inter', sans-serif;
  letter-spacing: -0.5px;
}

.brand-tagline {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-family: 'Inter', sans-serif;
}

.footer-section h4 {
  color: white;
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  font-family: 'Inter', sans-serif;
  position: relative;
  padding-bottom: 0.5rem;
}

.footer-section h4::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 30px;
  height: 2px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 2px;
}

.footer-section p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.7;
  margin-bottom: 2rem;
  font-family: 'Inter', sans-serif;
  font-size: 0.95rem;
}

.footer-section ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-section ul li {
  margin-bottom: 0.8rem;
}

.footer-section ul li a {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  font-weight: 500;
  position: relative;
  padding-left: 0;
}

.footer-section ul li a::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  transition: width 0.3s ease;
}

.footer-section ul li a:hover {
  color: white;
  padding-left: 15px;
  transform: translateX(5px);
}

.footer-section ul li a:hover::before {
  width: 10px;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 45px;
  height: 45px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  transition: left 0.3s ease;
  z-index: -1;
}

.social-link:hover::before {
  left: 0;
}

.social-link:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
  border-color: transparent;
}

.social-link.facebook:hover {
  color: #1877f2;
}

.social-link.instagram:hover {
  color: #e4405f;
}

.social-link.twitter:hover {
  color: #1da1f2;
}

.social-link.linkedin:hover {
  color: #0077b5;
}

.social-link svg {
  transition: transform 0.3s ease;
  color: rgba(255, 255, 255, 0.8);
}

.social-link:hover svg {
  transform: scale(1.1);
  color: white;
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 2rem;
}

.footer-bottom-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-bottom-content p {
  color: rgba(255, 255, 255, 0.7);
  margin: 0;
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  font-weight: 500;
}

.footer-bottom-links {
  display: flex;
  gap: 2rem;
}

.footer-bottom-links a {
  color: rgba(255, 255, 255, 0.6);
  text-decoration: none;
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  font-weight: 500;
  transition: color 0.3s ease;
}

.footer-bottom-links a:hover {
  color: #667eea;
}

/* Our Clients Section */
.clients-section {
  padding: 5rem 0;
  background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 50%, #cbd5e1 100%);
  position: relative;
  overflow: hidden;
}

.clients-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 20%, rgba(102, 126, 234, 0.08) 0%, transparent 50%),
              radial-gradient(circle at 70% 80%, rgba(118, 75, 162, 0.06) 0%, transparent 50%);
  pointer-events: none;
}

.clients-section .container {
  position: relative;
  z-index: 2;
}

.clients-section .section-title {
  background: linear-gradient(135deg, #1e293b 0%, #475569 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', sans-serif;
  font-weight: 700;
  text-align: center;
  margin-bottom: 1rem;
}

.clients-section .section-subtitle {
  color: rgba(30, 41, 59, 0.8);
  text-align: center;
  font-size: 1.1rem;
  margin-bottom: 3rem;
  font-family: 'Inter', sans-serif;
}

.clients-marquee {
  overflow: hidden;
  position: relative;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 2rem 0;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
}

.marquee-track {
  display: flex;
  animation: marquee 20s linear infinite;
  gap: 2.5rem;
  align-items: center;
}

.client-logo {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 15px;
  padding: 1.8rem 2.4rem;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.client-logo::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.5s ease;
}

.client-logo:hover::before {
  left: 100%;
}

.client-logo:hover {
  transform: translateY(-3px) scale(1.03);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.12);
}

.client-logo svg {
  height: 80px;
  width: auto;
  max-width: 200px;
  object-fit: contain;
  transition: all 0.3s ease;
}

.client-logo:hover svg {
  transform: scale(1.05);
}

@keyframes marquee {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

/* Pause animation on hover */
.clients-marquee:hover .marquee-track {
  animation-play-state: paused;
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
@media (max-width: 1200px) {
  .hero-content {
    grid-template-columns: 1fr;
    gap: 3rem;
    text-align: center;
  }
  
  .hero-visual {
    order: -1;
  }
  
  .hero-stats {
    justify-content: center;
  }
  
  .hero-buttons {
    justify-content: center;
  }
  
  .features-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }
  
  .testimonials-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 1024px) {
  .navbar .container {
    padding: 0 15px;
  }
  
  .nav-brand h2 {
    font-size: 1.8rem;
  }
  
  .nav-links {
    gap: 0.25rem;
  }
  
  .nav-link {
    padding: 0.75rem 1.25rem;
    font-size: 0.9rem;
  }
  
  .cart-dropdown {
    width: 320px;
    right: 15px;
  }
  
  .container {
    padding: 0 20px;
  }
  
  .hero {
    padding: 120px 0 80px;
  }
  
  .hero-title {
    font-size: 3rem;
  }
  
  .hero-subtitle {
    font-size: 1.1rem;
  }
  
  .section {
    padding: 60px 0;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .testimonials-grid {
    grid-template-columns: 1fr;
  }
  
  .furniture-slider-section {
    padding: 60px 0;
  }
  
  .slide-content {
    min-height: 500px;
  }
  
  .slide-info {
    padding: 50px 40px;
  }
  
  .slide-info h3 {
    font-size: 2.2rem;
  }
}

@media (max-width: 768px) {
  .hero-content,
  .about-content,
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .container {
    padding: 0 15px;
  }
  
  .hero {
    padding: 100px 0 60px;
  }
  
  .hero-content {
    gap: 2rem;
  }
  
  .hero-title {
    font-size: 2.5rem;
    line-height: 1.2;
  }
  
  .hero-subtitle {
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  
  .hero-stats {
    flex-direction: column;
    gap: 1rem;
  }
  
  .stat-divider {
    display: none;
  }
  
  .hero-buttons {
    flex-direction: column;
    gap: 1rem;
    width: 100%;
  }
  
  .btn {
    width: 100%;
    justify-content: center;
  }
  
  .hero-image-container {
    max-width: 100%;
  }
  
  .image-cards-container {
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
  }
  
  .section {
    padding: 50px 0;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .section-subtitle {
    font-size: 1rem;
  }
  
  .features-grid {
    gap: 1.5rem;
  }
  
  .feature-card {
    padding: 2rem 1.5rem;
  }
  
  .feature-icon {
    width: 60px;
    height: 60px;
    font-size: 1.5rem;
  }
  
  .feature-title {
    font-size: 1.3rem;
  }
  
  .navbar {
    padding: 0.75rem 0;
  }
  
  .nav-brand h2 {
    font-size: 1.6rem;
  }
  
  .nav-links {
    gap: 0.25rem;
  }
  
  .nav-link {
    padding: 0.625rem 1rem;
    font-size: 0.875rem;
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
    width: 300px;
    right: 10px;
    top: 70px;
  }
  
  .modal-body {
    grid-template-columns: 1fr;
  }

  /* Slider responsive */
  .furniture-slider-section {
    padding: 50px 0;
  }
  
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
  
  .slide-price {
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
  
  /* Clients section responsive */
  .clients-section {
    padding: 40px 0;
  }
  
  .clients-section .section-title {
    font-size: 2rem;
  }
  
  .clients-section .section-subtitle {
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  
  .clients-marquee {
    padding: 1.5rem 0;
  }
  
  .marquee-track {
    gap: 2rem;
  }
  
  .client-logo {
    padding: 1rem 1.5rem;
  }
  
  .client-logo img {
    height: 40px;
    max-width: 100px;
  }
  
  /* Form buttons responsive */
  .form-buttons {
    flex-direction: column;
    gap: 0.75rem;
  }
  
  .form-buttons .btn {
    min-width: auto;
  }
  
  /* Footer responsive */
  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
    margin-bottom: 2rem;
  }
  
  .footer-brand {
    max-width: none;
  }
  
  .brand-logo h3 {
    font-size: 1.8rem;
  }
  
  .social-links {
    justify-content: flex-start;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }
  
  .footer-bottom-links {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 10px;
  }
  
  .hero {
    padding: 80px 0 40px;
  }
  
  .hero-title {
    font-size: 2rem;
    line-height: 1.1;
  }
  
  .hero-subtitle {
    font-size: 0.9rem;
    margin-bottom: 1.5rem;
  }
  
  .hero-stats {
    gap: 0.75rem;
  }
  
  .stat-item {
    text-align: center;
  }
  
  .stat-number {
    font-size: 1.5rem;
  }
  
  .stat-label {
    font-size: 0.8rem;
  }
  
  .image-cards-container {
    grid-template-columns: 1fr;
    gap: 0.75rem;
  }
  
  .section {
    padding: 40px 0;
  }
  
  .section-title {
    font-size: 1.8rem;
  }
  
  .section-subtitle {
    font-size: 0.9rem;
  }
  
  .feature-card {
    padding: 1.5rem 1rem;
  }
  
  .feature-icon {
    width: 50px;
    height: 50px;
    font-size: 1.2rem;
  }
  
  .feature-title {
    font-size: 1.1rem;
  }
  
  .feature-description {
    font-size: 0.9rem;
  }
  
  .navbar {
    padding: 0.5rem 0;
  }
  
  .nav-brand h2 {
    font-size: 1.4rem;
  }
  
  .nav-links {
    display: none;
  }
  
  .nav-icons {
    gap: 0.375rem;
  }
  
  .icon-btn {
    width: 32px;
    height: 32px;
    font-size: 0.9rem;
  }
  
  .cart-count {
    width: 18px;
    height: 18px;
    font-size: 0.65rem;
    top: -6px;
    right: -6px;
  }
  
  .cart-dropdown {
    width: calc(100vw - 20px);
    right: 10px;
    left: 10px;
    top: 60px;
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
  
  /* Clients section mobile */
  .clients-section {
    padding: 30px 0;
  }
  
  .clients-section .section-title {
    font-size: 1.8rem;
  }
  
  .clients-section .section-subtitle {
    font-size: 0.9rem;
    margin-bottom: 1.5rem;
  }
  
  .clients-marquee {
    padding: 1rem 0;
    border-radius: 15px;
  }
  
  .marquee-track {
    gap: 1.5rem;
  }
  
  .client-logo {
    padding: 0.8rem 1.2rem;
    border-radius: 12px;
  }
  
  .client-logo img {
    height: 35px;
    max-width: 80px;
  }
  
  .footer-brand .brand-logo h3 {
    font-size: 1.5rem;
  }
  
  .footer-links h4 {
    font-size: 1rem;
  }
  
  .footer-links a {
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .hero-title {
    font-size: 1.8rem;
  }
  
  .section-title {
    font-size: 1.6rem;
  }
  
  .btn {
    padding: 0.75rem 1.5rem;
    font-size: 0.9rem;
  }
  
  .feature-card {
    padding: 1.25rem 0.75rem;
  }
  
  .slide-info {
    padding: 20px 15px;
  }
  
  .slide-info h3 {
    font-size: 1.3rem;
  }
  
  .slide-price {
    font-size: 1.3rem;
  }
}

/* Product Detail Modal Styles */
.product-detail-modal {
  background: white;
  border-radius: 20px;
  max-width: 1000px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
}

.product-detail-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  padding: 2rem;
}

.product-gallery .main-image {
  width: 100%;
  height: 400px;
  border-radius: 15px;
  overflow: hidden;
  margin-bottom: 1rem;
}

.product-gallery .main-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.thumbnail-gallery {
  display: flex;
  gap: 0.5rem;
}

.thumbnail {
  width: 80px;
  height: 60px;
  border-radius: 8px;
  object-fit: cover;
  cursor: pointer;
  border: 2px solid transparent;
  transition: border-color 0.3s ease;
}

.thumbnail:hover {
  border-color: #007bff;
}

.product-info h2 {
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 1rem;
}

.product-description {
  color: #666;
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.price-section {
  margin-bottom: 2rem;
}

.current-price {
  font-size: 2.5rem;
  font-weight: bold;
  color: #e67e22;
}

.features-section, .specifications-section {
  margin-bottom: 2rem;
}

.features-section h3, .specifications-section h3 {
  font-size: 1.3rem;
  color: #2c3e50;
  margin-bottom: 1rem;
}

.features-list {
  list-style: none;
  padding: 0;
}

.features-list li {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  color: #555;
}

.feature-icon {
  color: #27ae60;
  font-weight: bold;
  margin-right: 0.5rem;
}

.spec-grid {
  display: grid;
  gap: 0.8rem;
}

.spec-item {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
  border-bottom: 1px solid #eee;
}

.spec-label {
  font-weight: 600;
  color: #2c3e50;
}

.spec-value {
  color: #666;
}

.action-buttons {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

.add-to-cart-btn, .wishlist-btn {
  flex: 1;
  padding: 1rem 1.5rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  transition: all 0.3s ease;
}

.add-to-cart-btn {
  background: linear-gradient(135deg, #27ae60, #2ecc71);
  color: white;
  border: none;
}

.add-to-cart-btn:hover {
  background: linear-gradient(135deg, #229954, #27ae60);
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(39, 174, 96, 0.3);
}

.wishlist-btn {
  background: white;
  color: #e74c3c;
  border: 2px solid #e74c3c;
}

.wishlist-btn:hover {
  background: #e74c3c;
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(231, 76, 60, 0.3);
}

/* Mobile responsive for product detail modal */
@media (max-width: 768px) {
  .product-detail-modal {
    width: 95%;
    max-height: 95vh;
  }
  
  .product-detail-content {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    padding: 1.5rem;
  }
  
  .product-gallery .main-image {
    height: 300px;
  }
  
  .product-info h2 {
    font-size: 1.5rem;
  }
  
  .current-price {
    font-size: 2rem;
  }
  
  .action-buttons {
    flex-direction: column;
  }
  
  /* WhatsApp Agents Mobile Responsive */
  .whatsapp-agents-compact {
    margin: 20px 0;
    padding: 15px;
  }
  
  .agents-logos {
    gap: 15px;
  }
  
  .agent-logo {
    min-width: 70px;
    padding: 12px;
  }
  
  .logo-icon {
    width: 35px;
    height: 35px;
  }
  
  .agents-title-compact {
    font-size: 1.1rem;
  }

  .whatsapp-agents {
    margin-top: 2rem;
    padding: 1.5rem;
  }
  
  .agents-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
  
  .agent-card {
    padding: 1.25rem;
  }
  
  .agents-title {
    font-size: 1.5rem;
  }
  
  .agents-subtitle {
    font-size: 1rem;
  }
}
</style>