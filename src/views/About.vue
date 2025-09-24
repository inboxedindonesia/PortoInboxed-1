<template>
  <div class="about-page">
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
          <li><router-link to="/about" class="nav-link active">About</router-link></li>
          <li><router-link to="/contact" class="nav-link">Contact</router-link></li>
        </ul>
      </div>
    </nav>

    <!-- About Header -->
    <section class="about-header">
      <div class="container">
        <h1>About LuxeFurniture</h1>
        <p>Crafting premium furniture for over 25 years</p>
      </div>
    </section>

    <!-- About Content -->
    <section class="about-content">
      <div class="container">
        <div class="about-grid">
          <div class="about-text">
            <h2>Our Story</h2>
            <p>
              Founded in 1999, LuxeFurniture has been at the forefront of premium furniture design and manufacturing. 
              What started as a small family business has grown into a trusted name in luxury home furnishing, 
              serving customers worldwide with exceptional quality and timeless designs.
            </p>
            <p>
              Our commitment to excellence is reflected in every piece we create. From the selection of premium materials 
              to the meticulous craftsmanship, we ensure that each furniture item meets the highest standards of quality 
              and durability.
            </p>
          </div>
          <div class="about-image">
            <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=600&h=400&fit=crop" alt="Our Workshop">
          </div>
        </div>
      </div>
    </section>

    <!-- Values Section -->
    <section class="values-section">
      <div class="container">
        <h2>Our Values</h2>
        <div class="values-grid">
          <div class="value-card">
            <div class="value-icon">🎯</div>
            <h3>Quality First</h3>
            <p>We never compromise on quality. Every piece is crafted with precision and attention to detail.</p>
          </div>
          <div class="value-card">
            <div class="value-icon">🌱</div>
            <h3>Sustainability</h3>
            <p>We're committed to sustainable practices and eco-friendly materials in all our products.</p>
          </div>
          <div class="value-card">
            <div class="value-icon">💡</div>
            <h3>Innovation</h3>
            <p>We continuously innovate to bring you the latest in furniture design and functionality.</p>
          </div>
          <div class="value-card">
            <div class="value-icon">🤝</div>
            <h3>Customer Focus</h3>
            <p>Your satisfaction is our priority. We provide exceptional service from purchase to delivery.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section class="team-section">
      <div class="container">
        <h2>Meet Our Team</h2>
        <div class="team-grid">
          <div class="team-member">
            <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=300&h=300&fit=crop&crop=face" alt="John Smith">
            <h3>John Smith</h3>
            <p>Founder & CEO</p>
            <p>With over 30 years in furniture design, John leads our vision for premium quality furniture.</p>
          </div>
          <div class="team-member">
            <img src="https://images.unsplash.com/photo-1494790108755-2616b612b786?w=300&h=300&fit=crop&crop=face" alt="Sarah Johnson">
            <h3>Sarah Johnson</h3>
            <p>Head of Design</p>
            <p>Sarah brings creativity and innovation to every design, ensuring our furniture is both beautiful and functional.</p>
          </div>
          <div class="team-member">
            <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=300&h=300&fit=crop&crop=face" alt="Michael Brown">
            <h3>Michael Brown</h3>
            <p>Production Manager</p>
            <p>Michael oversees our manufacturing process, ensuring every piece meets our high-quality standards.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="stats-section">
      <div class="container">
        <div class="stats-grid">
          <div class="stat-item">
            <h3>25+</h3>
            <p>Years of Experience</p>
          </div>
          <div class="stat-item">
            <h3>10,000+</h3>
            <p>Happy Customers</p>
          </div>
          <div class="stat-item">
            <h3>500+</h3>
            <p>Furniture Designs</p>
          </div>
          <div class="stat-item">
            <h3>50+</h3>
            <p>Countries Served</p>
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
  name: 'About'
}
</script>

<style scoped>
.about-page {
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

/* About Header */
.about-header {
  padding: 120px 0 60px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
}

.about-header h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  font-weight: 700;
}

.about-header p {
  font-size: 1.2rem;
  opacity: 0.9;
}

/* About Content */
.about-content {
  padding: 80px 0;
}

.about-content .container {
  display: block;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-text h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.about-text p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #7f8c8d;
  margin-bottom: 1.5rem;
}

.about-image img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

/* Values Section */
.values-section {
  padding: 80px 0;
  background: #f8f9fa;
}

.values-section .container {
  display: block;
}

.values-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.value-card {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.value-card:hover {
  transform: translateY(-5px);
}

.value-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.value-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.value-card p {
  color: #7f8c8d;
  line-height: 1.6;
}

/* Team Section */
.team-section {
  padding: 80px 0;
}

.team-section .container {
  display: block;
}

.team-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.team-member {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.team-member:hover {
  transform: translateY(-5px);
}

.team-member img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1rem;
  border: 4px solid #3498db;
}

.team-member h3 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.team-member p:first-of-type {
  color: #3498db;
  font-weight: 600;
  margin-bottom: 1rem;
}

.team-member p:last-of-type {
  color: #7f8c8d;
  line-height: 1.6;
}

/* Stats Section */
.stats-section {
  padding: 80px 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.stats-section .container {
  display: block;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
}

.stat-item {
  text-align: center;
}

.stat-item h3 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
}

.stat-item p {
  font-size: 1.2rem;
  opacity: 0.9;
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
  
  .about-header h1 {
    font-size: 2rem;
  }
  
  .about-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .values-grid,
  .team-grid,
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .about-text h2,
  .values-section h2,
  .team-section h2 {
    font-size: 2rem;
  }
}
</style>