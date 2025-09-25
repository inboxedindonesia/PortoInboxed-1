<template>
  <div class="contact-page">
    <Header />

    <!-- Contact Header -->
    <section class="contact-header">
      <div class="container">
        <h1>Contact Us</h1>
        <p>Get in touch with our team for any inquiries</p>
      </div>
    </section>

    <!-- Contact Content -->
    <section class="contact-content">
      <div class="container">
        <div class="contact-grid">
          <!-- Contact Form -->
          <div class="contact-form-section">
            <h2>Send us a Message</h2>
            <form @submit.prevent="submitForm" class="contact-form">
              <div class="form-group">
                <label for="name">Full Name *</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="form.name" 
                  required
                  placeholder="Enter your full name"
                >
              </div>
              
              <div class="form-group">
                <label for="email">Email Address *</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="form.email" 
                  required
                  placeholder="Enter your email address"
                >
              </div>
              
              <div class="form-group">
                <label for="phone">Phone Number</label>
                <input 
                  type="tel" 
                  id="phone" 
                  v-model="form.phone"
                  placeholder="Enter your phone number"
                >
              </div>
              
              <div class="form-group">
                <label for="subject">Subject *</label>
                <select id="subject" v-model="form.subject" required>
                  <option value="">Select a subject</option>
                  <option value="general">General Inquiry</option>
                  <option value="product">Product Information</option>
                  <option value="order">Order Support</option>
                  <option value="complaint">Complaint</option>
                  <option value="partnership">Partnership</option>
                </select>
              </div>
              
              <div class="form-group">
                <label for="message">Message *</label>
                <textarea 
                  id="message" 
                  v-model="form.message" 
                  required
                  rows="5"
                  placeholder="Enter your message here..."
                ></textarea>
              </div>
              
              <button type="submit" class="submit-btn" :disabled="isSubmitting">
                {{ isSubmitting ? 'Sending...' : 'Send Message' }}
              </button>
            </form>
          </div>

          <!-- Contact Information -->
          <div class="contact-info-section">
            <h2>Get in Touch</h2>
            <div class="contact-info">
              <div class="info-item">
                <div class="info-icon">📍</div>
                <div class="info-content">
                  <h3>Address</h3>
                  <p>123 Furniture Street<br>Design City, DC 12345<br>United States</p>
                </div>
              </div>
              
              <div class="info-item">
                <div class="info-icon">📞</div>
                <div class="info-content">
                  <h3>Phone</h3>
                  <p>+1 (555) 123-4567<br>+1 (555) 987-6543</p>
                </div>
              </div>
              
              <div class="info-item">
                <div class="info-icon">📧</div>
                <div class="info-content">
                  <h3>Email</h3>
                  <p>info@luxefurniture.com<br>support@luxefurniture.com</p>
                </div>
              </div>
              
              <div class="info-item">
                <div class="info-icon">🕒</div>
                <div class="info-content">
                  <h3>Business Hours</h3>
                  <p>Monday - Friday: 9:00 AM - 6:00 PM<br>Saturday: 10:00 AM - 4:00 PM<br>Sunday: Closed</p>
                </div>
              </div>
            </div>

            <!-- Social Media -->
            <div class="social-media">
              <h3>Follow Us</h3>
              <div class="social-links">
                <a href="https://facebook.com/luxefurniture" target="_blank" class="social-link" @click="openSocialMedia('facebook')">📘 Facebook</a>
                <a href="https://instagram.com/luxefurniture" target="_blank" class="social-link" @click="openSocialMedia('instagram')">📷 Instagram</a>
                <a href="https://twitter.com/luxefurniture" target="_blank" class="social-link" @click="openSocialMedia('twitter')">🐦 Twitter</a>
                <a href="https://linkedin.com/company/luxefurniture" target="_blank" class="social-link" @click="openSocialMedia('linkedin')">💼 LinkedIn</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Map Section -->
    <section class="map-section">
      <div class="container">
        <h2>Find Our Showroom</h2>
        <div class="map-placeholder">
          <div class="map-content">
            <h3>📍 LuxeFurniture Showroom</h3>
            <p>Visit our showroom to see our furniture collection in person</p>
            <p><strong>Address:</strong> 123 Furniture Street, Design City, DC 12345</p>
            <button class="directions-btn" @click="getDirections">Get Directions</button>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="faq-section">
      <div class="container">
        <h2>Frequently Asked Questions</h2>
        <div class="faq-grid">
          <div class="faq-item" v-for="(faq, index) in faqs" :key="index">
            <div class="faq-question" @click="toggleFaq(index)">
              <h3>{{ faq.question }}</h3>
              <span class="faq-toggle">{{ faq.isOpen ? '−' : '+' }}</span>
            </div>
            <div class="faq-answer" v-show="faq.isOpen">
              <p>{{ faq.answer }}</p>
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
  name: 'Contact',
  components: {
    Header,
    Footer
  },
  data() {
    return {
      isScrolled: false,
      showCartDropdown: false,
      cart: [],
      isSubmitting: false,
      form: {
        name: '',
        email: '',
        phone: '',
        subject: '',
        message: ''
      },
      faqs: [
        {
          question: 'What is your return policy?',
          answer: 'We offer a 30-day return policy for all furniture items in original condition. Custom orders are non-returnable.',
          isOpen: false
        },
        {
          question: 'Do you offer delivery services?',
          answer: 'Yes, we provide free delivery within 50 miles of our showroom. Additional charges apply for longer distances.',
          isOpen: false
        },
        {
          question: 'Can I customize furniture pieces?',
          answer: 'Absolutely! We offer customization options for most of our furniture pieces including fabric, color, and size modifications.',
          isOpen: false
        },
        {
          question: 'What payment methods do you accept?',
          answer: 'We accept all major credit cards, PayPal, bank transfers, and offer financing options for purchases over $1,000.',
          isOpen: false
        },
        {
          question: 'How long does delivery take?',
          answer: 'Standard delivery takes 2-4 weeks. Custom orders may take 6-8 weeks depending on the complexity of customization.',
          isOpen: false
        }
      ]
    }
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0)
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50
    },
    removeFromCart(itemId) {
      this.cart = this.cart.filter(item => item.id !== itemId)
    },
    proceedToCheckout() {
      alert('Proceeding to checkout...')
      this.showCartDropdown = false
    },
    async submitForm() {
      this.isSubmitting = true
      
      // Simulate form submission
      try {
        await new Promise(resolve => setTimeout(resolve, 2000))
        
        alert('Thank you for your message! We will get back to you within 24 hours.')
        
        // Reset form
        this.form = {
          name: '',
          email: '',
          phone: '',
          subject: '',
          message: ''
        }
      } catch (error) {
        alert('Sorry, there was an error sending your message. Please try again.')
      } finally {
        this.isSubmitting = false
      }
    },
    
    toggleFaq(index) {
      this.faqs[index].isOpen = !this.faqs[index].isOpen
    },
    
    getDirections() {
      const address = "123 Furniture Street, Design City, DC 12345, United States"
      const encodedAddress = encodeURIComponent(address)
      const googleMapsUrl = `https://www.google.com/maps/search/?api=1&query=${encodedAddress}`
      window.open(googleMapsUrl, '_blank')
    },
    
    openSocialMedia(platform) {
      const urls = {
        facebook: 'https://facebook.com/luxefurniture',
        instagram: 'https://instagram.com/luxefurniture',
        twitter: 'https://twitter.com/luxefurniture',
        linkedin: 'https://linkedin.com/company/luxefurniture'
      }
      
      if (urls[platform]) {
        window.open(urls[platform], '_blank')
      }
    },
    
    increaseQuantity(itemId) {
      const item = this.cart.find(item => item.id === itemId)
      if (item) {
        item.quantity++
      }
    },
    
    decreaseQuantity(itemId) {
      const item = this.cart.find(item => item.id === itemId)
      if (item && item.quantity > 1) {
        item.quantity--
      }
    }
  }
}
</script>

<style scoped>
.contact-page {
  min-height: 100vh;
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
  padding: 0.75rem;
  border-radius: 50%;
  color: #667eea;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  backdrop-filter: blur(10px);
}

.icon-btn:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
  color: white;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: 600;
  box-shadow: 0 2px 8px rgba(239, 68, 68, 0.3);
}

.nav-link:hover,
.nav-link.active {
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
  transform: translateY(-2px);
}

/* Contact Header */
.contact-header {
  padding: 5rem 0 3rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.contact-header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.1) 0%, transparent 60%),
              radial-gradient(circle at 70% 80%, rgba(255, 255, 255, 0.08) 0%, transparent 60%);
  z-index: 1;
}

.contact-header .container {
  position: relative;
  z-index: 2;
}

.contact-header h1 {
  font-size: 3.5rem;
  margin-bottom: 1.5rem;
  font-weight: 700;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  letter-spacing: -1px;
}

.contact-header p {
  font-size: 1.3rem;
  opacity: 0.9;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 400;
  line-height: 1.6;
}

/* Contact Content */
.contact-content {
  padding: 8rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
  position: relative;
}

.contact-content::before {
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

.contact-content .container {
  display: block;
  position: relative;
  z-index: 2;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
}

/* Contact Form */
.contact-form-section h2 {
  font-size: 2.2rem;
  margin-bottom: 2.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.contact-form {
  background: rgba(255, 255, 255, 0.9);
  padding: 3rem;
  border-radius: 25px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.form-group {
  margin-bottom: 2rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.75rem;
  font-weight: 600;
  color: #475569;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 0.95rem;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 1rem 1.25rem;
  border: 2px solid rgba(102, 126, 234, 0.1);
  border-radius: 15px;
  font-size: 1rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-sizing: border-box;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
  background: rgba(255, 255, 255, 1);
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.15);
}

.form-group textarea {
  resize: vertical;
  min-height: 140px;
}

.submit-btn {
  width: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 1.2rem;
  border-radius: 25px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  position: relative;
  overflow: hidden;
}

.submit-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.6s ease;
}

.submit-btn:hover::before {
  left: 100%;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(102, 126, 234, 0.4);
}

.submit-btn:disabled {
  background: #94a3b8;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

/* Contact Info */
.contact-info-section h2 {
  font-size: 2.2rem;
  margin-bottom: 2.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.contact-info {
  margin-bottom: 3.5rem;
}

.info-item {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 20px;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.info-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.12);
  background: rgba(255, 255, 255, 1);
}

.info-icon {
  font-size: 2.2rem;
  min-width: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  filter: drop-shadow(0 4px 15px rgba(102, 126, 234, 0.3));
}

.info-content h3 {
  margin: 0 0 0.75rem 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 1.3rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.info-content p {
  margin: 0;
  color: #64748b;
  line-height: 1.7;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 1rem;
}

/* Social Media */
.social-media h3 {
  margin-bottom: 1rem;
  color: #2c3e50;
}

.social-links {
  display: flex;
  gap: 1.5rem;
  margin-top: 2.5rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 50%;
  text-decoration: none;
  font-size: 1.5rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
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
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.5s;
}

.social-link:hover::before {
  left: 100%;
}

.social-link:hover {
  transform: translateY(-8px) scale(1.1);
  box-shadow: 0 20px 40px rgba(102, 126, 234, 0.4);
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
}

/* Map Section */
.map-section {
  padding: 4rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
}

.map-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 70%, rgba(102, 126, 234, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 70% 30%, rgba(118, 75, 162, 0.1) 0%, transparent 50%);
  pointer-events: none;
}

.map-section .container {
  display: block;
  position: relative;
  z-index: 2;
}

.map-section h2 {
  text-align: center;
  font-size: 2.2rem;
  margin-bottom: 2.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.map-placeholder {
  background: rgba(255, 255, 255, 0.9);
  border-radius: 20px;
  padding: 3rem;
  text-align: center;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.map-placeholder:hover {
  transform: translateY(-5px);
  box-shadow: 0 30px 70px rgba(0, 0, 0, 0.15);
}

.map-content h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.map-content p {
  color: #64748b;
  margin-bottom: 1rem;
  line-height: 1.6;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.directions-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 1rem 2.5rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  position: relative;
  overflow: hidden;
}

.directions-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.6s ease;
}

.directions-btn:hover::before {
  left: 100%;
}

.directions-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(102, 126, 234, 0.4);
}

/* FAQ Section */
.faq-section {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 5rem 0;
  position: relative;
}

.faq-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 20% 80%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 80% 20%, rgba(255, 255, 255, 0.1) 0%, transparent 50%);
  pointer-events: none;
}

.faq-section .container {
  display: block;
  position: relative;
  z-index: 2;
}

.faq-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: white;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 700;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  letter-spacing: -0.02em;
}

.faq-grid {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  margin-bottom: 1.5rem;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.faq-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.15);
  background: rgba(255, 255, 255, 1);
}

.faq-question {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.faq-question:hover {
  background: rgba(102, 126, 234, 0.05);
}

.faq-question h3 {
  margin: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 1.2rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 600;
}

.faq-toggle {
  font-size: 1.5rem;
  font-weight: bold;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  transition: transform 0.3s ease;
}

.faq-answer {
  padding: 0 2rem 2rem;
  border-top: 1px solid rgba(102, 126, 234, 0.1);
}

.faq-answer p {
  margin: 0;
  color: #64748b;
  line-height: 1.7;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 1rem;
}

/* Footer */
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

/* Responsive */
@media (max-width: 1200px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  
  .footer-content {
    grid-template-columns: repeat(2, 1fr);
    gap: 40px;
  }
}

@media (max-width: 1024px) {
  .container {
    padding: 0 20px;
  }
  
  .contact-header {
    padding: 120px 0 80px;
  }
  
  .contact-header h1 {
    font-size: 2.5rem;
  }
  
  .contact-header p {
    font-size: 1.1rem;
  }
  
  .contact-section {
    padding: 80px 0;
  }
  
  .contact-info {
    padding: 2.5rem;
  }
  
  .contact-form {
    padding: 2.5rem;
  }
  
  .form-group {
    margin-bottom: 1.5rem;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: 32px;
    padding: 70px 0 40px;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 15px;
  }
  
  .nav-links {
    gap: 1rem;
  }
  
  .contact-header {
    padding: 100px 0 60px;
  }
  
  .contact-header h1 {
    font-size: 2rem;
    line-height: 1.2;
  }
  
  .contact-header p {
    font-size: 1rem;
  }
  
  .contact-section {
    padding: 60px 0;
  }
  
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .contact-info {
    padding: 2rem 1.5rem;
  }
  
  .contact-form {
    padding: 2rem 1.5rem;
  }
  
  .contact-info h3 {
    font-size: 1.3rem;
  }
  
  .contact-form h3 {
    font-size: 1.3rem;
  }
  
  .info-item {
    padding: 1rem;
  }
  
  .info-item h4 {
    font-size: 1rem;
  }
  
  .info-item p {
    font-size: 0.9rem;
  }
  
  .form-group {
    margin-bottom: 1.25rem;
  }
  
  .form-group label {
    font-size: 0.9rem;
  }
  
  .form-group input,
  .form-group textarea {
    font-size: 0.9rem;
    padding: 12px 16px;
  }
  
  .btn-submit {
    padding: 12px 24px;
    font-size: 0.9rem;
  }
  
  .social-links {
    flex-direction: row;
    flex-wrap: wrap;
    gap: 12px;
  }
  
  .social-link {
    width: 36px;
    height: 36px;
  }
  
  .map-placeholder {
    padding: 2rem;
    min-height: 250px;
  }
  
  .map-placeholder h4 {
    font-size: 1.1rem;
  }
  
  .map-placeholder p {
    font-size: 0.9rem;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: 32px;
    padding: 60px 0 32px;
  }
  
  .footer-brand h3 {
    font-size: 1.3rem;
  }
  
  .footer-section h4 {
    font-size: 1rem;
  }
  
  .footer-section a {
    font-size: 0.9rem;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
    gap: 12px;
  }
  
  .footer-bottom-links {
    justify-content: center;
    gap: 16px;
  }
  
  .footer-bottom p,
  .footer-bottom-links a {
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 10px;
  }
  
  .contact-header {
    padding: 80px 0 40px;
  }
  
  .contact-header h1 {
    font-size: 1.8rem;
    line-height: 1.1;
  }
  
  .contact-header p {
    font-size: 0.9rem;
  }
  
  .contact-section {
    padding: 50px 0;
  }
  
  .contact-info {
    padding: 1.5rem 1rem;
  }
  
  .contact-form {
    padding: 1.5rem 1rem;
  }
  
  .contact-info h3,
  .contact-form h3 {
    font-size: 1.2rem;
  }
  
  .info-item {
    padding: 0.75rem;
  }
  
  .info-item h4 {
    font-size: 0.95rem;
  }
  
  .info-item p {
    font-size: 0.85rem;
  }
  
  .form-group {
    margin-bottom: 1rem;
  }
  
  .form-group label {
    font-size: 0.85rem;
  }
  
  .form-group input,
  .form-group textarea {
    font-size: 0.85rem;
    padding: 10px 14px;
  }
  
  .btn-submit {
    padding: 10px 20px;
    font-size: 0.85rem;
    width: 100%;
  }
  
  .social-links {
    gap: 10px;
  }
  
  .social-link {
    width: 32px;
    height: 32px;
  }
  
  .map-placeholder {
    padding: 1.5rem;
    min-height: 200px;
  }
  
  .map-placeholder h4 {
    font-size: 1rem;
  }
  
  .map-placeholder p {
    font-size: 0.85rem;
  }
  
  .footer-content {
    padding: 50px 0 24px;
    gap: 24px;
  }
  
  .footer-brand h3 {
    font-size: 1.2rem;
  }
  
  .footer-brand p {
    font-size: 0.85rem;
  }
  
  .footer-section h4 {
    font-size: 0.95rem;
  }
  
  .footer-section a {
    font-size: 0.85rem;
  }
  
  .footer-bottom-links {
    gap: 12px;
  }
  
  .footer-bottom p,
  .footer-bottom-links a {
    font-size: 0.8rem;
  }
}

@media (max-width: 360px) {
  .contact-header h1 {
    font-size: 1.6rem;
  }
  
  .contact-info,
  .contact-form {
    padding: 1.25rem 0.75rem;
  }
  
  .contact-info h3,
  .contact-form h3 {
    font-size: 1.1rem;
  }
  
  .info-item {
    padding: 0.5rem;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 8px 12px;
  }
  
  .map-placeholder {
    padding: 1.25rem;
  }
  
  .footer-brand h3 {
    font-size: 1.1rem;
  }
}
</style>