<template>
  <div class="contact-page">
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
          <li><router-link to="/catalog" class="nav-link">Catalog</router-link></li>
          <li><router-link to="/about" class="nav-link">About</router-link></li>
          <li><router-link to="/contact" class="nav-link active">Contact</router-link></li>
        </ul>
      </div>
    </nav>

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
                <a href="#" class="social-link">📘 Facebook</a>
                <a href="#" class="social-link">📷 Instagram</a>
                <a href="#" class="social-link">🐦 Twitter</a>
                <a href="#" class="social-link">💼 LinkedIn</a>
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
            <button class="directions-btn">Get Directions</button>
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
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <h3>LuxeFurniture</h3>
            <p>Premium furniture for your dream home</p>
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
            <p>📧 info@luxefurniture.com</p>
            <p>📞 +1 (555) 123-4567</p>
            <p>📍 123 Furniture St, Design City</p>
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
  name: 'Contact',
  data() {
    return {
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
  methods: {
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
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  z-index: 1000;
  padding: 1rem 0;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand .brand-link {
  text-decoration: none;
  color: inherit;
}

.nav-brand h2 {
  color: #2c3e50;
  margin: 0;
  font-size: 1.8rem;
  font-weight: 700;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
  align-items: center;
}

.nav-link {
  color: #2c3e50;
  text-decoration: none;
  font-weight: 500;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  transition: all 0.3s ease;
}

.nav-link:hover,
.nav-link.active {
  color: #3498db;
  background: rgba(52, 152, 219, 0.1);
}

/* Contact Header */
.contact-header {
  padding: 120px 0 60px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
}

.contact-header h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  font-weight: 700;
}

.contact-header p {
  font-size: 1.2rem;
  opacity: 0.9;
}

/* Contact Content */
.contact-content {
  padding: 80px 0;
}

.contact-content .container {
  display: block;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
}

/* Contact Form */
.contact-form-section h2 {
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.contact-form {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 12px;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: #2c3e50;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
  box-sizing: border-box;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #3498db;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  width: 100%;
  background: #3498db;
  color: white;
  border: none;
  padding: 1rem;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.submit-btn:hover:not(:disabled) {
  background: #2980b9;
}

.submit-btn:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
}

/* Contact Info */
.contact-info-section h2 {
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.contact-info {
  margin-bottom: 3rem;
}

.info-item {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
  padding: 1.5rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.info-icon {
  font-size: 2rem;
  min-width: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.info-content h3 {
  margin: 0 0 0.5rem 0;
  color: #2c3e50;
  font-size: 1.2rem;
}

.info-content p {
  margin: 0;
  color: #7f8c8d;
  line-height: 1.6;
}

/* Social Media */
.social-media h3 {
  margin-bottom: 1rem;
  color: #2c3e50;
}

.social-links {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.social-link {
  color: #3498db;
  text-decoration: none;
  padding: 0.5rem;
  border-radius: 8px;
  transition: background 0.3s ease;
}

.social-link:hover {
  background: rgba(52, 152, 219, 0.1);
}

/* Map Section */
.map-section {
  padding: 80px 0;
  background: #f8f9fa;
}

.map-section .container {
  display: block;
}

.map-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.map-placeholder {
  background: white;
  border-radius: 12px;
  padding: 3rem;
  text-align: center;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.map-content h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.map-content p {
  color: #7f8c8d;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.directions-btn {
  background: #3498db;
  color: white;
  border: none;
  padding: 0.75rem 2rem;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.directions-btn:hover {
  background: #2980b9;
}

/* FAQ Section */
.faq-section {
  padding: 80px 0;
}

.faq-section .container {
  display: block;
}

.faq-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.faq-grid {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  background: white;
  border-radius: 12px;
  margin-bottom: 1rem;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.faq-question {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  cursor: pointer;
  transition: background 0.3s ease;
}

.faq-question:hover {
  background: #f8f9fa;
}

.faq-question h3 {
  margin: 0;
  color: #2c3e50;
  font-size: 1.1rem;
}

.faq-toggle {
  font-size: 1.5rem;
  font-weight: bold;
  color: #3498db;
}

.faq-answer {
  padding: 0 1.5rem 1.5rem;
  border-top: 1px solid #eee;
}

.faq-answer p {
  margin: 0;
  color: #7f8c8d;
  line-height: 1.6;
}

/* Footer */
.footer {
  background: #2c3e50;
  color: white;
  padding: 3rem 0 1rem;
}

.footer .container {
  display: block;
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
  color: #3498db;
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
  color: #3498db;
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #34495e;
  color: #bdc3c7;
}

/* Responsive */
@media (max-width: 768px) {
  .nav-links {
    gap: 1rem;
  }
  
  .contact-header h1 {
    font-size: 2rem;
  }
  
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .social-links {
    flex-direction: row;
    flex-wrap: wrap;
  }
  
  .map-placeholder {
    padding: 2rem;
  }
}
</style>