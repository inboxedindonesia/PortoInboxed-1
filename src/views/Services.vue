<template>
  <div class="services-page">
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
          <li><router-link to="/services" class="nav-link active">Services</router-link></li>
          <li><router-link to="/catalog" class="nav-link">Catalog</router-link></li>
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

    <!-- Services Header -->
    <section class="services-header">
      <div class="container">
        <h1>Our Services</h1>
        <p>Comprehensive furniture solutions tailored to your needs</p>
      </div>
    </section>

    <!-- Service Packages -->
    <section class="service-packages">
      <div class="container">
        <h2>Service Packages</h2>
        <div class="packages-grid">
          <div v-for="servicePackage in servicePackages" :key="servicePackage.id" class="package-card">
          <div class="package-icon">
            {{ servicePackage.icon }}
          </div>
          <div class="package-content">
            <h3>{{ servicePackage.name }}</h3>
            <p class="package-description">{{ servicePackage.description }}</p>
            <div class="package-features">
              <ul>
                <li v-for="feature in servicePackage.features" :key="feature">
                  <i class="fas fa-check"></i>
                  {{ feature }}
                </li>
              </ul>
            </div>
            <div class="package-pricing">
              <span class="price">{{ servicePackage.price }}</span>
              <span class="duration">{{ servicePackage.duration }}</span>
            </div>
            <button class="package-btn" @click="selectPackage(servicePackage)">
              {{ servicePackage.buttonText }}
            </button>
          </div>
        </div>
        </div>
      </div>
    </section>

    <!-- Additional Services -->
    <section class="additional-services">
      <div class="container">
        <h2>Additional Services</h2>
        <div class="services-grid">
          <div v-for="service in additionalServices" :key="service.id" class="service-card">
            <div class="service-image">
              <img :src="service.image" :alt="service.name">
            </div>
            <div class="service-info">
              <h3>{{ service.name }}</h3>
              <p>{{ service.description }}</p>
              <div class="service-price">
                <span>{{ service.price }}</span>
              </div>
              <button class="service-btn" @click="bookService(service)">
                Book Now
              </button>
            </div>
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
            <p>Creating beautiful spaces with premium furniture and exceptional service.</p>
          </div>
          <div class="footer-section">
            <h4>Quick Links</h4>
            <ul>
              <li><router-link to="/">Home</router-link></li>
              <li><router-link to="/services">Services</router-link></li>
              <li><router-link to="/catalog">Catalog</router-link></li>
              <li><router-link to="/about">About</router-link></li>
              <li><router-link to="/contact">Contact</router-link></li>
            </ul>
          </div>
          <div class="footer-section">
            <h4>Contact Info</h4>
            <p>📍 123 Furniture Street, Design City</p>
            <p>📞 (555) 123-4567</p>
            <p>✉️ info@luxefurniture.com</p>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2024 LuxeFurniture. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'Services',
  data() {
    return {
      showCartDropdown: false,
      cart: [],
      servicePackages: [
        {
          id: 1,
          name: 'Interior Design Package',
          description: 'Complete interior design consultation and planning for your space.',
          icon: '🎨',
          price: 'Starting from $2,500',
          duration: '4-6 weeks',
          buttonText: 'Get Quote',
          features: [
            '3D Room Visualization',
            'Color Scheme Planning',
            'Furniture Selection Guide',
            'Space Optimization',
            'Style Consultation'
          ]
        },
        {
          id: 2,
          name: 'Installation & Assembly',
          description: 'Professional furniture installation and assembly service.',
          icon: '🔧',
          price: 'Starting from $150',
          duration: '1-2 days',
          buttonText: 'Book Service',
          features: [
            'Expert Assembly Team',
            'Tool & Equipment Included',
            'Quality Guarantee',
            'Clean-up Service',
            'Same-day Service Available'
          ]
        },
        {
          id: 3,
          name: 'Maintenance & Care',
          description: 'Regular maintenance to keep your furniture in perfect condition.',
          icon: '🛠️',
          price: 'Starting from $99/month',
          duration: 'Ongoing',
          buttonText: 'Subscribe',
          features: [
            'Monthly Inspection',
            'Cleaning & Polishing',
            'Minor Repairs',
            'Fabric Protection',
            'Priority Support'
          ]
        },
        {
          id: 4,
          name: 'Custom Furniture',
          description: 'Bespoke furniture designed and crafted to your specifications.',
          icon: '✨',
          price: 'Quote on Request',
          duration: '6-12 weeks',
          buttonText: 'Consult Now',
          features: [
            'Custom Design Process',
            'Premium Materials',
            'Handcrafted Quality',
            'Unique Pieces',
            'Lifetime Warranty'
          ]
        },
        {
          id: 5,
          name: 'Space Planning',
          description: 'Optimize your space layout for maximum functionality and aesthetics.',
          icon: '📐',
          price: 'Starting from $800',
          duration: '2-3 weeks',
          buttonText: 'Plan Space',
          features: [
            'Floor Plan Analysis',
            'Traffic Flow Optimization',
            'Storage Solutions',
            'Lighting Design',
            'Ergonomic Considerations'
          ]
        },
        {
          id: 6,
          name: 'Relocation Service',
          description: 'Complete furniture moving and setup service for your new space.',
          icon: '🚚',
          price: 'Starting from $500',
          duration: '1-3 days',
          buttonText: 'Get Moving',
          features: [
            'Professional Packing',
            'Safe Transportation',
            'Furniture Protection',
            'Setup & Arrangement',
            'Insurance Coverage'
          ]
        }
      ],
      additionalServices: [
        {
          id: 1,
          name: 'Express Delivery',
          description: 'Get your furniture delivered within 24-48 hours.',
          price: 'From $50',
          image: 'https://images.unsplash.com/photo-1566576912321-d58ddd7a6088?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
        },
        {
          id: 2,
          name: 'Virtual Consultation',
          description: 'Online design consultation from the comfort of your home.',
          price: 'From $100',
          image: 'https://images.unsplash.com/photo-1600880292203-757bb62b4baf?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
        },
        {
          id: 3,
          name: 'Warranty Extension',
          description: 'Extend your furniture warranty up to 5 years.',
          price: 'From $75',
          image: 'https://images.unsplash.com/photo-1560472354-b33ff0c44a43?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
        },
        {
          id: 4,
          name: 'Trade-In Program',
          description: 'Trade your old furniture for credit towards new purchases.',
          price: 'Up to 30% credit',
          image: 'https://images.unsplash.com/photo-1586023492125-27b2c045efd7?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
        }
      ]
    }
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0)
    }
  },
  methods: {
    removeFromCart(productId) {
      this.cart = this.cart.filter(item => item.id !== productId)
    },
    proceedToCheckout() {
      alert('Proceeding to checkout...')
      this.showCartDropdown = false
    },
    selectPackage(servicePackage) {
      alert(`You selected: ${servicePackage.name}. We'll contact you soon for consultation!`)
    },
    bookService(service) {
      alert(`Booking ${service.name}. Our team will contact you to schedule the service.`)
    }
  }
}
</script>

<style scoped>
.services-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Navigation Styles */
.navbar {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 20px;
}

.nav-brand .brand-link {
  text-decoration: none;
  color: #2c3e50;
}

.nav-brand h2 {
  margin: 0;
  font-size: 1.8rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  align-items: center;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: #2c3e50;
  font-weight: 500;
  padding: 0.5rem 1rem;
  border-radius: 25px;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link:hover,
.nav-link.active {
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
}

.nav-icons {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.icon-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: all 0.3s ease;
  position: relative;
}

.icon-btn:hover {
  background: rgba(102, 126, 234, 0.1);
  transform: scale(1.1);
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: #e74c3c;
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

/* Cart Dropdown */
.cart-dropdown {
  position: absolute;
  top: 100%;
  right: 20px;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  width: 350px;
  max-height: 400px;
  overflow-y: auto;
  z-index: 1001;
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
  color: #2c3e50;
}

.close-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #7f8c8d;
}

.cart-items {
  padding: 1rem;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #f8f9fa;
}

.cart-item-image {
  width: 50px;
  height: 50px;
  object-fit: cover;
  border-radius: 8px;
}

.cart-item-info {
  flex: 1;
}

.cart-item-info h4 {
  margin: 0 0 0.25rem 0;
  font-size: 0.9rem;
  color: #2c3e50;
}

.cart-item-info p {
  margin: 0;
  font-size: 0.8rem;
  color: #7f8c8d;
}

.remove-btn {
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 50%;
  width: 25px;
  height: 25px;
  cursor: pointer;
  font-size: 0.9rem;
}

.cart-total {
  text-align: center;
  padding: 1rem 0;
  border-top: 2px solid #eee;
  margin-top: 1rem;
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

.empty-cart {
  padding: 2rem;
  text-align: center;
  color: #7f8c8d;
}

/* Services Header */
.services-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 4rem 0;
  text-align: center;
}

.services-header h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  font-weight: 700;
}

.services-header p {
  font-size: 1.2rem;
  opacity: 0.9;
  max-width: 600px;
  margin: 0 auto;
}

/* Service Packages */
.service-packages {
  padding: 4rem 0;
}

.service-packages h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.packages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.package-card {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.package-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  border-color: #667eea;
}

.package-icon {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 1rem;
}

.package-content h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c3e50;
  text-align: center;
}

.package-description {
  color: #7f8c8d;
  margin-bottom: 1.5rem;
  text-align: center;
  line-height: 1.6;
}

.package-features ul {
  list-style: none;
  padding: 0;
  margin-bottom: 2rem;
}

.package-features li {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.check-icon {
  color: #27ae60;
  font-weight: bold;
  margin-right: 0.5rem;
}

.package-pricing {
  text-align: center;
  margin-bottom: 2rem;
}

.price {
  display: block;
  font-size: 1.3rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 0.5rem;
}

.duration {
  color: #7f8c8d;
  font-size: 0.9rem;
}

.package-btn {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 1rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 1rem;
}

.package-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Additional Services */
.additional-services {
  background: #f8f9fa;
  padding: 4rem 0;
}

.additional-services h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.service-card {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.service-image {
  height: 200px;
  overflow: hidden;
}

.service-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.service-card:hover .service-image img {
  transform: scale(1.1);
}

.service-info {
  padding: 1.5rem;
}

.service-info h3 {
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.service-info p {
  color: #7f8c8d;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.service-price {
  font-size: 1.2rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 1rem;
}

.service-btn {
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

.service-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

/* Footer */
.footer {
  background: #2c3e50;
  color: white;
  padding: 3rem 0 1rem;
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
  color: #ecf0f1;
}

.footer-section p {
  color: #bdc3c7;
  line-height: 1.6;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin-bottom: 0.5rem;
}

.footer-section ul li a {
  color: #bdc3c7;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section ul li a:hover {
  color: #667eea;
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #34495e;
  color: #bdc3c7;
}

/* Responsive Design */
@media (max-width: 768px) {
  .navbar .container {
    flex-direction: column;
    gap: 1rem;
  }

  .nav-links {
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
  }

  .services-header h1 {
    font-size: 2rem;
  }

  .packages-grid {
    grid-template-columns: 1fr;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .cart-dropdown {
    width: 300px;
    right: 10px;
  }
}
</style>