# HealthyLife Medical Center - Comprehensive API Documentation

## Table of Contents
- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [CSS Framework & Design System](#css-framework--design-system)
- [JavaScript APIs & Functions](#javascript-apis--functions)
- [HTML Components](#html-components)
- [Forms & User Interactions](#forms--user-interactions)
- [Responsive Design](#responsive-design)
- [Deployment](#deployment)
- [Usage Examples](#usage-examples)
- [Customization Guide](#customization-guide)

## Project Overview

HealthyLife Medical Center is a modern, responsive single-page website for a medical facility. The project provides a complete healthcare website solution with appointment booking, service information, doctor profiles, and contact functionality.

### Key Features
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **Interactive UI**: Smooth animations, form validation, and dynamic content
- **Modern Styling**: CSS Grid, Flexbox, and custom properties
- **Accessibility**: Semantic HTML and keyboard navigation support
- **Performance**: Optimized loading with preloader and lazy loading concepts

### Technology Stack
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Libraries**: jQuery 3.6.0, Slick Carousel 1.8.1, Font Awesome 6.0.0, Animate.css 4.1.1
- **Deployment**: GitHub Pages via GitHub Actions

## Architecture

```
HealthyLife Medical Center/
├── docter.html              # Main application file
├── *.jpg                    # Doctor profile images
├── .github/
│   └── workflows/
│       └── static.yml       # GitHub Pages deployment
└── API_DOCUMENTATION.md     # This documentation
```

## CSS Framework & Design System

### CSS Custom Properties (Design Tokens)

The website uses a comprehensive design system with CSS custom properties:

```css
:root {
    --primary-color: #28a745;     /* Main brand color (green) */
    --secondary-color: #fbfbfb;   /* Secondary brand color */
    --accent-color: #ffc107;      /* Accent color (yellow) */
    --light-color: #f8f9fa;       /* Light background */
    --dark-color: #343a40;        /* Dark text */
    --text-color: #495057;        /* Body text */
    --white: #ffffff;             /* Pure white */
    --shadow: 0 5px 15px rgba(0, 0, 0, 0.1);  /* Standard shadow */
    --transition: all 0.3s ease;  /* Standard transition */
}
```

### Component Classes

#### Layout Components

**`.hero`**
- **Purpose**: Main landing section with call-to-action
- **Features**: Full viewport height, gradient background, floating animations
- **Usage**: 
```html
<section class="hero" id="home">
    <div class="hero-content">
        <h2>Your Health Is Our Priority</h2>
        <p>Experience world-class healthcare...</p>
        <div class="btn-container">
            <a href="#appointment" class="btn btn-primary">Book Appointment</a>
        </div>
    </div>
</section>
```

**`.section-title`**
- **Purpose**: Standardized section headers
- **Features**: Centered text with accent underline
- **Usage**:
```html
<div class="section-title">
    <h2>Section Title</h2>
    <p>Section description</p>
</div>
```

#### Navigation Components

**`header`**
- **Purpose**: Fixed navigation header with responsive mobile menu
- **States**: `.scrolled` class added on scroll for transparency effect
- **Features**: Auto-hiding mobile menu, active link highlighting

**`.mobile-menu-btn`**
- **Purpose**: Mobile hamburger menu toggle
- **Responsive**: Hidden on desktop, visible on mobile (≤768px)

#### Button Components

**`.btn`**
- **Base Class**: All buttons inherit from this class
- **Variants**:
  - `.btn-primary`: White background with primary color text
  - `.btn-secondary`: Transparent with white border
  - `.submit-btn`: Form submission button with primary styling

**Usage Example**:
```html
<a href="#contact" class="btn btn-primary">Primary Button</a>
<button type="submit" class="submit-btn">Submit Form</button>
```

#### Card Components

**`.service-card`**
- **Purpose**: Service information display cards
- **Features**: Hover animations, image overlays, pricing display
- **Structure**:
```html
<div class="service-card">
    <div class="service-image">
        <img src="image.jpg" alt="Service">
    </div>
    <div class="service-content">
        <h3>Service Title</h3>
        <p>Service description</p>
        <div class="service-price">From 70000 LKR</div>
        <a href="#appointment" class="service-btn">Book Now</a>
    </div>
</div>
```

**`.doctor-card`**
- **Purpose**: Doctor profile display cards
- **Features**: Social media links, specialty display, hover effects
- **Structure**:
```html
<div class="doctor-card">
    <div class="doctor-image">
        <img src="doctor.jpg" alt="Doctor Name">
    </div>
    <div class="doctor-content">
        <h3>Dr. Name</h3>
        <span class="doctor-specialty">Specialty</span>
        <p>Doctor description</p>
        <div class="doctor-social">
            <a href="#"><i class="fab fa-twitter"></i></a>
        </div>
    </div>
</div>
```

#### Form Components

**`.form-group`**
- **Purpose**: Wrapper for form field and label
- **Usage**: Provides consistent spacing and structure

**`.form-control`**
- **Purpose**: Input field styling with focus states
- **Features**: Custom focus styles, border radius, transitions

## JavaScript APIs & Functions

### Core Application Functions

#### Preloader Management

**`window.addEventListener("load", function())`**
- **Purpose**: Manages the loading screen display
- **Behavior**: Shows spinner for 1 second, then fades out over 0.5 seconds
- **Usage**: Automatically triggered on page load

```javascript
// Preloader control
window.addEventListener("load", function() {
    const loader = document.getElementById("loader");
    setTimeout(function() {
        loader.style.opacity = "0";
        setTimeout(function() {
            loader.style.display = "none";
        }, 500);
    }, 1000);
});
```

#### Mobile Navigation

**Mobile Menu Toggle**
- **Target Element**: `#mobileMenuBtn`
- **Function**: Toggles mobile navigation visibility
- **Features**: Icon switching between hamburger and close (X)

```javascript
const mobileMenuBtn = document.getElementById("mobileMenuBtn");
const navbar = document.getElementById("navbar");

mobileMenuBtn.addEventListener("click", function() {
    navbar.classList.toggle("active");
    mobileMenuBtn.innerHTML = navbar.classList.contains("active") ? 
        '<i class="fas fa-times"></i>' : '<i class="fas fa-bars"></i>';
});
```

**Auto-Close Mobile Menu**
- **Trigger**: Clicking any navigation link
- **Purpose**: Improves mobile UX by auto-closing menu after selection

#### Scroll Behavior Functions

**Sticky Header**
```javascript
window.addEventListener("scroll", function() {
    if (window.scrollY > 100) {
        header.classList.add("scrolled");  // Adds transparency effect
    } else {
        header.classList.remove("scrolled");
    }
});
```

**Smooth Scrolling**
- **Target**: All anchor links (`a[href^="#"]`)
- **Behavior**: Smooth scroll to target section with 80px offset for fixed header

```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const targetElement = document.querySelector(this.getAttribute('href'));
        if (targetElement) {
            window.scrollTo({
                top: targetElement.offsetTop - 80,
                behavior: 'smooth'
            });
        }
    });
});
```

**Active Navigation Highlighting**
- **Purpose**: Highlights current section in navigation
- **Trigger**: Scroll position
- **Threshold**: 200px offset for early activation

#### Back to Top Functionality

**`#backToTop` Button**
- **Visibility**: Appears after 300px scroll
- **Behavior**: Smooth scroll to page top
- **Styling**: Fixed position with hover animations

```javascript
const backToTopBtn = document.getElementById("backToTop");
window.addEventListener("scroll", function() {
    if (window.pageYOffset > 300) {
        backToTopBtn.classList.add("active");
    } else {
        backToTopBtn.classList.remove("active");
    }
});
```

### Form Handling APIs

#### Appointment Form Submission

**Form ID**: `#appointmentForm`
**Function**: `appointmentForm.addEventListener("submit", function(e))`

**Form Fields**:
- `fullName` (required): Patient's full name
- `email` (required): Contact email
- `phone` (required): Phone number
- `dob` (required): Date of birth
- `appointmentDate` (required): Preferred appointment date
- `department` (required): Medical department selection
- `doctor` (optional): Preferred doctor
- `message` (optional): Additional information

**Data Structure**:
```javascript
const formData = {
    name: document.getElementById("fullName").value,
    email: document.getElementById("email").value,
    phone: document.getElementById("phone").value,
    dob: document.getElementById("dob").value,
    date: document.getElementById("appointmentDate").value,
    department: document.getElementById("department").value,
    doctor: document.getElementById("doctor").value,
    message: document.getElementById("message").value
};
```

**Usage Example**:
```javascript
// Custom form handler
document.getElementById("appointmentForm").addEventListener("submit", function(e) {
    e.preventDefault();
    // Process form data
    const formData = getFormData();
    submitAppointment(formData);
});
```

#### Newsletter Subscription

**Form ID**: `#newsletterForm`
**Purpose**: Email subscription for health tips and updates
**Validation**: Email format validation
**Behavior**: Form reset after successful submission

### Animation & UI Enhancement APIs

#### Floating Elements Animation

**Target**: `.floating-element`
**Function**: Randomized animation timing for visual appeal

```javascript
const floatingElements = document.querySelectorAll(".floating-element");
floatingElements.forEach((element, index) => {
    const duration = 6 + Math.random() * 4;  // 6-10 seconds
    const delay = Math.random() * 5;         // 0-5 seconds
    
    element.style.animationDuration = `${duration}s`;
    element.style.animationDelay = `${delay}s`;
});
```

#### Scroll-Triggered Animations

**Target Elements**: `.service-card`, `.doctor-card`, `.feature-item`
**Trigger**: Element enters viewport (1.3 screen height threshold)
**Animation**: Fade in from bottom using Animate.css

```javascript
const animateOnScroll = function() {
    const elements = document.querySelectorAll(".service-card, .doctor-card, .feature-item");
    
    elements.forEach(element => {
        const elementPosition = element.getBoundingClientRect().top;
        const screenPosition = window.innerHeight / 1.3;
        
        if (elementPosition < screenPosition) {
            element.classList.add("animate__animated", "animate__fadeInUp");
        }
    });
};
```

#### Testimonials Slider (jQuery/Slick)

**Configuration**:
```javascript
$('.testimonials-container').slick({
    dots: true,              // Navigation dots
    infinite: true,          // Loop slides
    speed: 300,             // Transition speed (ms)
    slidesToShow: 1,        // Single slide view
    adaptiveHeight: true,   // Adjust height to content
    autoplay: true,         // Auto-advance slides
    autoplaySpeed: 5000,    // 5-second intervals
    arrows: false           // Hide prev/next arrows
});
```

## HTML Components

### Page Structure

The website follows a single-page application structure with semantic HTML5:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Meta tags, title, external CSS -->
</head>
<body>
    <!-- Preloader -->
    <div class="loader" id="loader">...</div>
    
    <!-- Fixed Header with Navigation -->
    <header id="header">...</header>
    
    <!-- Main Content Sections -->
    <section class="hero" id="home">...</section>
    <section class="about-section" id="about">...</section>
    <section class="services-section" id="services">...</section>
    <section class="doctors-section" id="doctors">...</section>
    <section class="appointment-section" id="appointment">...</section>
    <section class="contact-section" id="contact">...</section>
    
    <!-- Footer -->
    <footer>...</footer>
    
    <!-- Back to Top Button -->
    <div class="back-to-top" id="backToTop">...</div>
    
    <!-- JavaScript -->
    <script>...</script>
</body>
</html>
```

### Section Components

#### Header Component
```html
<header id="header">
    <div class="logo">
        <div class="logo-icon"><i class="fas fa-heartbeat"></i></div>
        <h1>Healthy<span>Life</span></h1>
    </div>
    <nav id="navbar">
        <ul>
            <li><a href="#home" class="nav-link active">Home</a></li>
            <!-- Additional nav items -->
        </ul>
    </nav>
    <button class="mobile-menu-btn" id="mobileMenuBtn">
        <i class="fas fa-bars"></i>
    </button>
</header>
```

#### Services Grid Component
```html
<div class="services-container">
    <div class="service-card">
        <div class="service-image">
            <img src="service-image.jpg" alt="Service Name">
        </div>
        <div class="service-content">
            <h3>Service Title</h3>
            <p>Service description...</p>
            <div class="service-price">From 70000 LKR</div>
            <a href="#appointment" class="service-btn">Book Now</a>
        </div>
    </div>
    <!-- Repeat for additional services -->
</div>
```

#### Contact Information Component
```html
<div class="contact-info">
    <h3>Get In Touch</h3>
    <div class="info-item">
        <div class="info-icon"><i class="fas fa-map-marker-alt"></i></div>
        <div class="info-content">
            <h4>Location</h4>
            <p>Batticaloa, Periyakallar</p>
        </div>
    </div>
    <!-- Additional contact items -->
</div>
```

## Forms & User Interactions

### Appointment Booking Form

**Purpose**: Allows patients to schedule medical appointments
**Validation**: HTML5 validation with custom styling
**Required Fields**: Name, email, phone, DOB, appointment date, department

#### Form Structure:
```html
<form id="appointmentForm">
    <div class="form-group">
        <label for="fullName">Full Name</label>
        <input type="text" id="fullName" class="form-control" required>
    </div>
    <!-- Additional form fields -->
    <div class="form-group">
        <button type="submit" class="submit-btn">Book Appointment</button>
    </div>
</form>
```

#### Department Options:
- General Medicine
- Cardiology
- Neurology
- Pediatrics
- Orthopedics
- Radiology
- Laboratory Services

#### Doctor Selection Options:
- Dr. Alan (Cardiologist)
- Dr. Siraj (Neurologist)
- Dr. Anupama (Pediatrician)
- Dr. Shageeth VSP (Orthopedic Surgeon)

### Newsletter Subscription

**Purpose**: Email collection for health updates
**Location**: Footer section
**Validation**: Email format validation

```html
<form id="newsletterForm">
    <div class="form-group">
        <input type="email" class="form-control" placeholder="Your Email" required>
    </div>
    <button type="submit" class="submit-btn">Subscribe</button>
</form>
```

## Responsive Design

### Breakpoints

The website uses a mobile-first responsive design approach:

#### Desktop (Default)
- **Target**: All screen sizes above 992px
- **Features**: Full navigation, multi-column layouts, hover effects

#### Tablet (≤992px)
```css
@media (max-width: 992px) {
    .hero h2 { font-size: 2.8rem; }
    nav ul { gap: 15px; }
}
```

#### Mobile (≤768px)
```css
@media (max-width: 768px) {
    .mobile-menu-btn { display: block; }
    nav { position: fixed; /* Mobile menu positioning */ }
    .hero { padding: 150px 5% 80px; }
    .btn-container { flex-direction: column; }
}
```

#### Small Mobile (≤576px)
```css
@media (max-width: 576px) {
    .hero h2 { font-size: 2rem; }
    .section-title h2 { font-size: 2rem; }
}
```

### Responsive Features

#### Grid Layouts
- **Services**: `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))`
- **Doctors**: `grid-template-columns: repeat(auto-fit, minmax(250px, 1fr))`
- **Contact**: `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))`

#### Flexible Components
- **About Section**: Flexbox with wrapping for image and content
- **Navigation**: Transforms to mobile-friendly vertical menu
- **Buttons**: Full-width on mobile devices

## Deployment

### GitHub Pages Configuration

The project uses GitHub Actions for automatic deployment to GitHub Pages:

**Workflow File**: `.github/workflows/static.yml`

#### Deployment Triggers:
- **Push to main branch**: Automatic deployment
- **Manual dispatch**: Can be triggered manually from GitHub Actions tab

#### Deployment Process:
1. **Checkout**: Retrieves latest code from repository
2. **Setup Pages**: Configures GitHub Pages environment
3. **Upload Artifact**: Packages entire repository
4. **Deploy**: Publishes to GitHub Pages URL

#### Permissions Required:
```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

### Deployment Steps:

1. **Push to Main Branch**:
```bash
git add .
git commit -m "Update website content"
git push origin main
```

2. **Automatic Deployment**: GitHub Actions will automatically deploy changes

3. **Access**: Website available at `https://[username].github.io/[repository-name]/`

## Usage Examples

### Basic Implementation

#### Adding a New Service:
```html
<div class="service-card">
    <div class="service-image">
        <img src="new-service.jpg" alt="New Service">
    </div>
    <div class="service-content">
        <h3>New Medical Service</h3>
        <p>Description of the new service offered...</p>
        <div class="service-price">From 50000 LKR</div>
        <a href="#appointment" class="service-btn">Book Now</a>
    </div>
</div>
```

#### Adding a New Doctor:
```html
<div class="doctor-card">
    <div class="doctor-image">
        <img src="new-doctor.jpg" alt="Dr. New Doctor">
    </div>
    <div class="doctor-content">
        <h3>Dr. New Doctor</h3>
        <span class="doctor-specialty">Specialty</span>
        <p>Doctor's background and experience...</p>
        <div class="doctor-social">
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-linkedin"></i></a>
            <a href="#"><i class="fas fa-envelope"></i></a>
        </div>
    </div>
</div>
```

### Customization Examples

#### Changing Color Scheme:
```css
:root {
    --primary-color: #007bff;     /* Blue instead of green */
    --accent-color: #28a745;      /* Green accent */
}
```

#### Adding Custom Animations:
```css
.custom-animation {
    animation: customSlide 2s ease-in-out;
}

@keyframes customSlide {
    0% { transform: translateX(-100%); opacity: 0; }
    100% { transform: translateX(0); opacity: 1; }
}
```

#### Custom Form Validation:
```javascript
function validateAppointmentForm(formData) {
    const errors = [];
    
    if (!formData.name.trim()) {
        errors.push("Name is required");
    }
    
    if (!isValidEmail(formData.email)) {
        errors.push("Valid email is required");
    }
    
    return errors;
}

function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}
```

## Customization Guide

### Adding New Sections

#### 1. HTML Structure:
```html
<section class="new-section" id="new-section">
    <div class="section-title">
        <h2>New Section Title</h2>
        <p>Section description</p>
    </div>
    <div class="new-section-content">
        <!-- Section content -->
    </div>
</section>
```

#### 2. CSS Styling:
```css
.new-section {
    padding: 100px 5%;
    background: var(--light-color);
}

.new-section-content {
    max-width: 1200px;
    margin: 50px auto 0;
}
```

#### 3. Navigation Link:
```html
<li><a href="#new-section" class="nav-link">New Section</a></li>
```

### Modifying Existing Components

#### Updating Contact Information:
1. **Location**: Update in the contact section HTML
2. **Phone Numbers**: Modify `href="tel:..."` attributes
3. **Email Addresses**: Update `href="mailto:..."` attributes
4. **Hours**: Modify the hours display text

#### Changing Service Prices:
```html
<div class="service-price">From [NEW_PRICE] LKR</div>
```

#### Adding Social Media Links:
```html
<div class="social-icons">
    <a href="https://facebook.com/yourpage"><i class="fab fa-facebook-f"></i></a>
    <a href="https://twitter.com/yourhandle"><i class="fab fa-twitter"></i></a>
    <!-- Add more social platforms -->
</div>
```

### Performance Optimization

#### Image Optimization:
- **Format**: Use WebP format for better compression
- **Lazy Loading**: Add `loading="lazy"` attribute to images
- **Responsive Images**: Use `srcset` for different screen sizes

#### CSS Optimization:
- **Critical CSS**: Inline critical styles in `<head>`
- **Non-critical CSS**: Load non-essential styles asynchronously
- **Minimize**: Remove unused CSS rules

#### JavaScript Optimization:
- **Lazy Loading**: Load non-critical scripts after page load
- **Debouncing**: Implement debouncing for scroll events
- **Modern Syntax**: Use ES6+ features for better performance

### Accessibility Improvements

#### ARIA Labels:
```html
<button class="mobile-menu-btn" aria-label="Toggle mobile menu">
    <i class="fas fa-bars"></i>
</button>
```

#### Focus Management:
```css
.btn:focus,
.form-control:focus {
    outline: 2px solid var(--primary-color);
    outline-offset: 2px;
}
```

#### Screen Reader Support:
```html
<img src="doctor.jpg" alt="Dr. John Smith, Cardiologist">
<a href="#appointment" aria-describedby="appointment-help">Book Appointment</a>
```

---

This documentation provides a comprehensive guide to the HealthyLife Medical Center website, covering all public APIs, components, and customization options. For additional support or custom modifications, refer to the individual code sections and examples provided above.