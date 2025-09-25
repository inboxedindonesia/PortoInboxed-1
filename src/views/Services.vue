<template>
  <div class="services-page">
    <Header />

    <!-- Services Header -->
    <section class="services-header">
      <div class="header-background">
        <div class="floating-shapes">
          <div class="shape shape-1"></div>
          <div class="shape shape-2"></div>
          <div class="shape shape-3"></div>
          <div class="shape shape-4"></div>
          <div class="shape shape-5"></div>
        </div>
        <div class="abstract-pattern">
          <svg viewBox="0 0 1200 400" class="pattern-svg">
            <defs>
              <linearGradient id="patternGradient" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:rgba(255,255,255,0.1);stop-opacity:1" />
                <stop offset="50%" style="stop-color:rgba(255,255,255,0.05);stop-opacity:1" />
                <stop offset="100%" style="stop-color:rgba(255,255,255,0.1);stop-opacity:1" />
              </linearGradient>
            </defs>
            <path d="M0,200 Q300,100 600,200 T1200,200 L1200,400 L0,400 Z" fill="url(#patternGradient)"/>
            <path d="M0,250 Q400,150 800,250 T1200,250 L1200,400 L0,400 Z" fill="rgba(255,255,255,0.03)"/>
          </svg>
        </div>
      </div>
      <div class="container">
        <h1>Our Services</h1>
        <p>Comprehensive furniture solutions tailored to your needs</p>
      </div>
    </section>

    <!-- Certifications & Standards -->
    <section class="certifications">
      <div class="container">
        <h2>Certifications & Standards</h2>
        <p>Trusted quality backed by international standards</p>
        <div class="certifications-grid">
          <div class="cert-item">
            <div class="cert-logo">
              <svg width="80" height="80" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <circle cx="50" cy="50" r="45" fill="#0066cc" stroke="#003d7a" stroke-width="2"/>
                <circle cx="50" cy="50" r="35" fill="none" stroke="#ffffff" stroke-width="2"/>
                <text x="50" y="40" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="12" font-weight="bold">ISO</text>
                <text x="50" y="55" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="10">9001</text>
                <text x="50" y="68" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="8">Quality</text>
              </svg>
            </div>
            <h4>ISO 9001</h4>
            <p>Quality Management System</p>
          </div>
          
          <div class="cert-item">
            <div class="cert-logo">
              <svg width="80" height="80" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <circle cx="50" cy="50" r="45" fill="#228b22" stroke="#006400" stroke-width="2"/>
                <circle cx="50" cy="50" r="35" fill="none" stroke="#ffffff" stroke-width="2"/>
                <text x="50" y="40" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="12" font-weight="bold">ISO</text>
                <text x="50" y="55" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="10">14001</text>
                <text x="50" y="68" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="8">Environment</text>
              </svg>
            </div>
            <h4>ISO 14001</h4>
            <p>Environmental Management</p>
          </div>
          
          <div class="cert-item">
            <div class="cert-logo">
              <svg width="80" height="80" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <rect x="10" y="10" width="80" height="80" rx="8" fill="#8b4513" stroke="#654321" stroke-width="2"/>
                <rect x="20" y="20" width="60" height="60" rx="4" fill="none" stroke="#ffffff" stroke-width="2"/>
                <text x="50" y="35" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="10" font-weight="bold">FSC</text>
                <path d="M35 45 L45 55 L65 35" stroke="#ffffff" stroke-width="3" fill="none" stroke-linecap="round"/>
                <text x="50" y="75" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="8">Certified</text>
              </svg>
            </div>
            <h4>FSC Certified</h4>
            <p>Sustainable Wood Sourcing</p>
          </div>
          
          <div class="cert-item">
            <div class="cert-logo">
              <svg width="80" height="80" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <circle cx="50" cy="50" r="45" fill="#dc143c" stroke="#8b0000" stroke-width="2"/>
                <circle cx="50" cy="50" r="35" fill="none" stroke="#ffffff" stroke-width="2"/>
                <text x="50" y="35" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="10" font-weight="bold">CARB</text>
                <text x="50" y="50" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="9">Phase 2</text>
                <text x="50" y="65" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="8">Compliant</text>
              </svg>
            </div>
            <h4>CARB Phase 2</h4>
            <p>Low Emission Standards</p>
          </div>
          
          <div class="cert-item">
            <div class="cert-logo">
              <svg width="80" height="80" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <polygon points="50,10 90,35 75,75 25,75 10,35" fill="#4169e1" stroke="#191970" stroke-width="2"/>
                <polygon points="50,20 80,40 70,70 30,70 20,40" fill="none" stroke="#ffffff" stroke-width="2"/>
                <text x="50" y="45" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="10" font-weight="bold">CE</text>
                <text x="50" y="60" text-anchor="middle" fill="#ffffff" font-family="Arial, sans-serif" font-size="8">Marking</text>
              </svg>
            </div>
            <h4>CE Marking</h4>
            <p>European Conformity</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Service Packages -->
    <section class="service-packages">
      <div class="container">
        <h2>Service Packages</h2>
        <div class="packages-grid">
          <div v-for="servicePackage in servicePackages" :key="servicePackage.id" class="package-card">
            <div class="package-image">
              <img :src="servicePackage.image" :alt="servicePackage.name" />
              <div class="package-overlay">
              </div>
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
    <Footer />
  </div>
</template>

<script>
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'Services',
  components: {
    Header,
    Footer
  },
  data() {
    return {
      showCartDropdown: false,
      cart: [],
      servicePackages: [
        {
          id: 1,
          name: 'Interior Design Package',
          description: 'Complete interior design consultation and planning for your space with expert guidance.',
          icon: '🎨',
          image: 'https://images.unsplash.com/photo-1586023492125-27b2c045efd7?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
          description: 'Professional furniture installation and assembly service by certified experts.',
          icon: '🔧',
          image: 'https://images.unsplash.com/photo-1581539250439-c96689b516dd?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
          description: 'Regular maintenance to keep your furniture in perfect condition year-round.',
          icon: '🛠️',
          image: 'https://images.unsplash.com/photo-1560472354-b33ff0c44a43?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
          description: 'Bespoke furniture designed and crafted to your exact specifications and style.',
          icon: '✨',
          image: 'https://images.unsplash.com/photo-1555041469-a586c61ea9bc?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
          description: 'Optimize your space layout for maximum functionality and aesthetic appeal.',
          icon: '📐',
          image: 'https://images.unsplash.com/photo-1600607687939-ce8a6c25118c?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
          description: 'Complete furniture moving and setup service for seamless transitions.',
          icon: '🚚',
          image: 'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80',
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
        },
        {
          id: 5,
          name: 'Custom Design Service',
          description: 'Create bespoke furniture pieces tailored to your exact specifications.',
          price: 'From $200',
          image: 'https://images.unsplash.com/photo-1586023492125-27b2c045efd7?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
        },
        {
          id: 6,
          name: 'Maintenance & Repair',
          description: 'Professional maintenance and repair services for your furniture.',
          price: 'From $80',
          image: 'https://images.unsplash.com/photo-1560472354-b33ff0c44a43?ixlib=rb-4.0.3&auto=format&fit=crop&w=400&q=80'
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
      // Show a more detailed confirmation with service details
      const confirmation = confirm(`Apakah Anda ingin memilih paket ${servicePackage.name}?\n\nHarga: ${servicePackage.price}\nDurasi: ${servicePackage.duration}\n\nKlik OK untuk melanjutkan atau Cancel untuk membatalkan.`)
      
      if (confirmation) {
        alert(`Terima kasih! Anda telah memilih paket ${servicePackage.name}. Tim kami akan menghubungi Anda dalam 24 jam untuk konsultasi lebih lanjut.`)
        // Here you could add logic to save the selection or redirect to a booking form
        console.log('Selected package:', servicePackage)
      }
    },
    bookService(service) {
      // Show a more detailed booking confirmation
      const confirmation = confirm(`Apakah Anda ingin memesan layanan ${service.name}?\n\nHarga: ${service.price}\nDeskripsi: ${service.description}\n\nKlik OK untuk melanjutkan pemesanan atau Cancel untuk membatalkan.`)
      
      if (confirmation) {
        alert(`Pemesanan berhasil! Layanan ${service.name} telah ditambahkan ke daftar pemesanan Anda. Tim kami akan menghubungi Anda untuk mengatur jadwal layanan.`)
        // Here you could add logic to save the booking or redirect to a booking form
        console.log('Booked service:', service)
      }
    },
    increaseQuantity(productId) {
      const item = this.cart.find(item => item.id === productId)
      if (item) {
        item.quantity++
      }
    },
    decreaseQuantity(productId) {
      const item = this.cart.find(item => item.id === productId)
      if (item && item.quantity > 1) {
        item.quantity--
      }
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
  gap: 1rem;
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
  padding: 6rem 0 4rem;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.header-background {
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
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 80px;
  height: 80px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
  background: linear-gradient(45deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.05));
}

.shape-2 {
  width: 120px;
  height: 120px;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.03));
}

.shape-3 {
  width: 60px;
  height: 60px;
  top: 30%;
  right: 30%;
  animation-delay: 4s;
  background: rgba(255, 255, 255, 0.08);
}

.shape-4 {
  width: 100px;
  height: 100px;
  bottom: 20%;
  left: 20%;
  animation-delay: 1s;
  background: linear-gradient(90deg, rgba(255, 255, 255, 0.12), rgba(255, 255, 255, 0.04));
}

.shape-5 {
  width: 140px;
  height: 140px;
  top: 10%;
  left: 50%;
  animation-delay: 3s;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.02));
}

@keyframes float {
  0%, 100% { 
    transform: translateY(0px) rotate(0deg);
    opacity: 0.7;
  }
  50% { 
    transform: translateY(-20px) rotate(180deg);
    opacity: 1;
  }
}

.abstract-pattern {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
}

.pattern-svg {
  width: 100%;
  height: 100%;
  position: absolute;
  bottom: 0;
}

.services-header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.15) 0%, transparent 60%),
              radial-gradient(circle at 70% 80%, rgba(255, 255, 255, 0.1) 0%, transparent 60%);
  z-index: 2;
}

.services-header .container {
  position: relative;
  z-index: 3;
}

.services-header h1 {
  font-size: 4rem;
  margin-bottom: 2rem;
  font-weight: 800;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  letter-spacing: -2px;
  line-height: 1.1;
}

.services-header p {
  font-size: 1.4rem;
  opacity: 0.95;
  max-width: 700px;
  margin: 0 auto;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 400;
  line-height: 1.7;
  letter-spacing: 0.3px;
}

/* Service Packages */
.service-packages {
  padding: 10rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
  position: relative;
}

.service-packages::before {
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

.service-packages .container {
  position: relative;
  z-index: 2;
}

.service-packages h2 {
  text-align: center;
  font-size: 3.2rem;
  margin-bottom: 5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 800;
  letter-spacing: -1px;
  line-height: 1.2;
}

.packages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
  gap: 3rem;
}

.package-card {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 25px;
  padding: 2rem;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.08);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  border: 1px solid rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  position: relative;
  overflow: hidden;
  max-width: 350px;
  margin: 0 auto;
}

.package-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(102, 126, 234, 0.05), transparent);
  transition: left 0.6s ease;
}

.package-card:hover::before {
  left: 100%;
}

.package-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 0 30px 70px rgba(0, 0, 0, 0.15);
  background: rgba(255, 255, 255, 1);
  border-color: rgba(102, 126, 234, 0.2);
}

.package-image {
  position: relative;
  width: 100%;
  height: 200px;
  border-radius: 15px;
  overflow: hidden;
  margin-bottom: 1.5rem;
}

.package-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.package-card:hover .package-image img {
  transform: scale(1.1);
}

.package-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.8) 0%, rgba(118, 75, 162, 0.8) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.package-card:hover .package-overlay {
  opacity: 1;
}

.package-icon {
  font-size: 4rem;
  color: white;
  text-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  animation: float 3s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

.package-content {
  padding: 0 1.5rem 1.5rem;
}

.package-content h3 {
  font-size: 1.6rem;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-align: center;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.package-description {
  color: #64748b;
  margin-bottom: 1.5rem;
  text-align: center;
  line-height: 1.6;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 0.95rem;
}

.package-features ul {
  list-style: none;
  padding: 0;
  margin-bottom: 2rem;
}

.package-features li {
  display: flex;
  align-items: center;
  margin-bottom: 0.6rem;
  color: #475569;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 0.9rem;
}

.check-icon {
  color: #10b981;
  font-weight: bold;
  margin-right: 0.75rem;
  font-size: 1.1rem;
}

.package-pricing {
  text-align: center;
  margin-bottom: 2rem;
  padding: 1.2rem;
  background: rgba(102, 126, 234, 0.05);
  border-radius: 12px;
  border: 1px solid rgba(102, 126, 234, 0.1);
}

.price {
  display: block;
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.duration {
  color: #64748b;
  font-size: 0.9rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 500;
}

.package-btn {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 1.2rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 1rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  position: relative;
  overflow: hidden;
}

.package-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.6s ease;
}

.package-btn:hover::before {
  left: 100%;
}

.package-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(102, 126, 234, 0.4);
}

/* Additional Services */
.additional-services {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 10rem 0;
  position: relative;
  overflow: hidden;
}

.additional-services::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.15) 0%, transparent 60%),
              radial-gradient(circle at 70% 80%, rgba(255, 255, 255, 0.1) 0%, transparent 60%);
  z-index: 1;
}

.additional-services .container {
  position: relative;
  z-index: 2;
}

.additional-services h2 {
  text-align: center;
  font-size: 3.2rem;
  margin-bottom: 5rem;
  color: white;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 800;
  letter-spacing: -1px;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  line-height: 1.2;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 3rem;
}

.service-card {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.service-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transition: left 0.6s ease;
  z-index: 1;
}

.service-card:hover::before {
  left: 100%;
}

.service-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 30px 70px rgba(0, 0, 0, 0.3);
  background: rgba(255, 255, 255, 0.25);
}

.service-image {
  height: 220px;
  overflow: hidden;
  position: relative;
}

.service-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
  filter: brightness(0.9);
}

.service-card:hover .service-image img {
  transform: scale(1.1);
  filter: brightness(1);
}

.service-info {
  padding: 2rem;
  position: relative;
  z-index: 2;
}

.service-info h3 {
  margin-bottom: 1rem;
  color: white;
  font-size: 1.4rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.service-info p {
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1.5rem;
  line-height: 1.7;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 0.95rem;
}

.service-price {
  font-size: 1.3rem;
  font-weight: 700;
  color: white;
  margin-bottom: 1.5rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.service-btn {
  width: 100%;
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  padding: 1rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  backdrop-filter: blur(10px);
  position: relative;
  overflow: hidden;
}

.service-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.6s ease;
}

.service-btn:hover::before {
  left: 100%;
}

.service-btn:hover {
  transform: translateY(-3px);
  background: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
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

/* Responsive Design */
@media (max-width: 1200px) {
  .packages-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }
  
  .services-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }
  
  .certifications-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
  }
}

@media (max-width: 1024px) {
  .container {
    padding: 0 20px;
  }
  
  .services-header {
    padding: 6rem 0 4rem;
  }
  
  .services-header h1 {
    font-size: 3rem;
  }
  
  .services-header p {
    font-size: 1.2rem;
  }
  
  .service-packages {
    padding: 7rem 0;
  }
  
  .service-packages h2 {
    font-size: 2.5rem;
  }
  
  .additional-services {
    padding: 7rem 0;
  }
  
  .additional-services h2 {
    font-size: 2.5rem;
  }
  
  .packages-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
  
  .services-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
  
  .certifications {
    padding: 70px 0;
  }
  
  .certifications h2 {
    font-size: 2.3rem;
  }
  
  .certifications-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 15px;
  }
  
  .navbar .container {
    flex-direction: column;
    gap: 1rem;
  }

  .nav-links {
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
  }

  .services-header {
    padding: 5rem 0 3rem;
  }

  .services-header h1 {
    font-size: 2.5rem;
    letter-spacing: -1px;
    line-height: 1.2;
  }

  .services-header p {
    font-size: 1.1rem;
    padding: 0 1rem;
  }

  .service-packages {
    padding: 6rem 0;
  }

  .service-packages h2 {
    font-size: 2.2rem;
    margin-bottom: 3rem;
  }

  .packages-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .package-image {
    height: 180px;
  }

  .package-card {
    max-width: 100%;
    padding: 1.5rem;
  }

  .package-content {
    padding: 0 1rem 1rem;
  }

  .package-content h3 {
    font-size: 1.4rem;
  }

  .additional-services {
    padding: 6rem 0;
  }

  .additional-services h2 {
    font-size: 2.2rem;
    margin-bottom: 3rem;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .service-image {
    height: 180px;
  }

  .cart-dropdown {
    width: 300px;
    right: 10px;
  }
  
  .certifications {
    padding: 60px 0;
  }
  
  .certifications h2 {
    font-size: 2rem;
  }
  
  .certifications p {
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  
  .certifications-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1.5rem;
  }
  
  .cert-item {
    padding: 1.5rem 1rem;
  }
  
  .cert-logo svg {
    width: 60px;
    height: 60px;
  }
  
  .cert-item h4 {
    font-size: 1.1rem;
  }
  
  .cert-item p {
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 10px;
  }
  
  .services-header {
    padding: 4rem 0 2.5rem;
  }

  .services-header h1 {
    font-size: 2rem;
    line-height: 1.1;
  }

  .services-header p {
    font-size: 1rem;
    padding: 0 0.5rem;
  }

  .service-packages {
    padding: 5rem 0;
  }

  .service-packages h2 {
    font-size: 1.8rem;
    margin-bottom: 2.5rem;
  }

  .package-card {
    padding: 1.25rem;
  }

  .package-content {
    padding: 0 0.75rem 0.75rem;
  }

  .package-content h3 {
    font-size: 1.2rem;
  }

  .package-content p {
    font-size: 0.9rem;
  }

  .additional-services {
    padding: 5rem 0;
  }

  .additional-services h2 {
    font-size: 1.8rem;
    margin-bottom: 2.5rem;
  }

  .service-card {
    padding: 1.25rem;
  }

  .service-content h3 {
    font-size: 1.2rem;
  }

  .service-content p {
    font-size: 0.9rem;
  }

  .service-image {
    height: 160px;
  }

  .package-image {
    height: 160px;
  }

  .cart-dropdown {
    width: 280px;
    right: 5px;
  }
  
  .certifications {
    padding: 50px 0;
  }
  
  .certifications h2 {
    font-size: 1.8rem;
  }
  
  .certifications p {
    font-size: 0.9rem;
    margin-bottom: 2rem;
  }
  
  .certifications-grid {
    grid-template-columns: 1fr;
    gap: 1.25rem;
  }
  
  .cert-item {
    padding: 1.25rem 0.75rem;
  }
  
  .cert-logo svg {
    width: 50px;
    height: 50px;
  }
  
  .cert-item h4 {
    font-size: 1rem;
  }
  
  .cert-item p {
    font-size: 0.8rem;
  }
}

@media (max-width: 360px) {
  .services-header h1 {
    font-size: 1.8rem;
  }

  .service-packages h2,
  .additional-services h2 {
    font-size: 1.6rem;
  }

  .package-card,
  .service-card {
    padding: 1rem;
  }

  .package-content,
  .service-content {
    padding: 0 0.5rem 0.5rem;
  }

  .package-content h3,
  .service-content h3 {
    font-size: 1.1rem;
  }

  .package-content p,
  .service-content p {
    font-size: 0.85rem;
  }
  
  .certifications h2 {
    font-size: 1.6rem;
  }
  
  .cert-item {
    padding: 1rem 0.5rem;
  }
}

/* Certifications Section */
.certifications {
  padding: 80px 0;
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
  position: relative;
}

.certifications::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="cert-pattern" x="0" y="0" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="1" fill="rgba(0,102,204,0.1)"/></pattern></defs><rect width="100" height="100" fill="url(%23cert-pattern)"/></svg>');
  opacity: 0.3;
}

.certifications .container {
  position: relative;
  z-index: 1;
}

.certifications h2 {
  text-align: center;
  font-size: 2.5rem;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-family: 'Inter', sans-serif;
}

.certifications p {
  text-align: center;
  font-size: 1.2rem;
  color: #6c757d;
  margin-bottom: 3rem;
  font-family: 'Inter', sans-serif;
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.cert-item {
  background: white;
  padding: 2rem 1.5rem;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  border: 1px solid rgba(0, 0, 0, 0.05);
  position: relative;
  overflow: hidden;
}

.cert-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.5s ease;
}

.cert-item:hover::before {
  left: 100%;
}

.cert-item:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.cert-logo {
  margin-bottom: 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.cert-logo svg {
  transition: transform 0.3s ease;
}

.cert-item:hover .cert-logo svg {
  transform: scale(1.1);
}

.cert-item h4 {
  font-size: 1.3rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 0.5rem;
  font-family: 'Inter', sans-serif;
}

.cert-item p {
  font-size: 0.95rem;
  color: #6c757d;
  margin: 0;
  font-family: 'Inter', sans-serif;
  line-height: 1.4;
}

@media (max-width: 768px) {
  .certifications {
    padding: 60px 0;
  }
  
  .certifications h2 {
    font-size: 2rem;
  }
  
  .certifications-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1.5rem;
  }
  
  .cert-item {
    padding: 1.5rem 1rem;
  }
  
  .cert-logo svg {
    width: 60px;
    height: 60px;
  }
}

</style>