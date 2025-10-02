name: "Sports Club Intercollege Competition Website with Unstop Integration"
description: |
  Build a responsive, modern website for a sports club's intercollege competition with minimal backend requirements and seamless Unstop integration for registrations and payments.

## Purpose
Create a professional, engaging website that serves as the central hub for an intercollege sports competition, handling event information, schedules, and redirecting registrations through Unstop's platform.

## Core Principles
1. **Minimal Backend**: Use static site approach with dynamic elements via JavaScript
2. **Unstop Integration**: Leverage Unstop's infrastructure for complex registration/payment handling
3. **Mobile-First**: Ensure excellent experience across all devices
4. **Easy Updates**: Structure for simple content management without technical expertise
5. **Performance**: Fast loading, optimized assets, CDN-friendly

---

## Goal
Build a complete sports competition website that attracts participants, provides clear information, and seamlessly integrates with Unstop for registration management while maintaining a professional, energetic sports aesthetic.

## Why
- **Event Management**: Centralize all competition information in one professional platform
- **Registration Simplification**: Outsource complex registration/payment to Unstop
- **Participant Experience**: Provide clear, accessible information to increase participation
- **Club Branding**: Establish professional presence for the sports club

## What
A responsive website featuring:
- Dynamic countdown timer and event highlights
- Comprehensive event information and schedules
- Sports/activities showcase with rules
- Seamless Unstop registration integration
- Gallery and social media integration
- Contact and venue information

### Success Criteria
- [ ] Website loads in under 3 seconds on mobile
- [ ] All pages responsive (320px to 4K displays)
- [ ] Unstop registration links working correctly
- [ ] Schedule downloadable as PDF
- [ ] Social media links integrated
- [ ] SEO optimized for event discovery
- [ ] Accessibility compliant (WCAG 2.1 Level AA)

## All Needed Context

### Documentation & References
```yaml
# Key Resources
- url: https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps
  why: PWA patterns for offline capability and performance
  
- url: https://web.dev/vitals/
  why: Core Web Vitals optimization for performance
  
- url: https://tailwindcss.com/docs
  why: Utility-first CSS framework for rapid, responsive design
  
- url: https://developers.google.com/maps/documentation/javascript/
  why: Embedded maps for venue location
  
- url: https://github.com/michalsnik/aos
  why: Animate on scroll library for dynamic effects
  
- url: https://swiperjs.com/get-started
  why: Touch-friendly gallery slider implementation

- url: https://developers.google.com/sheets/api
  why: Optional live schedule updates via Google Sheets

- pattern: Unstop Integration
  note: No API needed - simple redirect links to Unstop event page
  example: https://unstop.com/competitions/your-event-name
```

### Project Structure
```bash
sports-competition-website/
├── index.html                  # Home page
├── about.html                  # About the event
├── sports.html                 # Sports & activities
├── schedule.html               # Event schedule
├── gallery.html                # Photo gallery
├── contact.html                # Contact information
├── assets/
│   ├── css/
│   │   ├── main.css           # Main stylesheet
│   │   └── tailwind.css       # Tailwind utilities
│   ├── js/
│   │   ├── app.js            # Main JavaScript
│   │   ├── countdown.js       # Countdown timer
│   │   └── schedule.js        # Schedule interactions
│   ├── images/
│   │   ├── logo/              # Club and event logos
│   │   ├── sports/            # Sport-specific images
│   │   ├── gallery/           # Event photos
│   │   └── heroes/            # Hero section images
│   └── downloads/
│       └── schedule.pdf       # Downloadable schedule
├── components/                 # Reusable HTML components
│   ├── header.html            # Navigation header
│   └── footer.html            # Footer with links
├── data/
│   ├── sports.json            # Sports data
│   └── schedule.json          # Event schedule data
├── favicon.ico
├── robots.txt
├── sitemap.xml
└── README.md
```

### Known Implementation Considerations
```javascript
// CRITICAL: Browser compatibility - ensure ES6 features have fallbacks
// CRITICAL: Image optimization - use WebP with JPG fallbacks
// CRITICAL: Lazy loading for gallery images to improve performance
// CRITICAL: CORS considerations if fetching from Google Sheets
// CRITICAL: Mobile touch events for gallery swiper
// CRITICAL: Countdown timer timezone handling
// CRITICAL: Form validation before Unstop redirect
```

## Implementation Blueprint

### Data Models and Structure

```javascript
// Sports Data Structure (sports.json)
{
  "sports": [
    {
      "id": "cricket",
      "name": "Cricket",
      "icon": "🏏",
      "image": "/assets/images/sports/cricket.jpg",
      "description": "T20 format intercollege championship",
      "rules": [
        "Teams of 11 players",
        "20 overs per side",
        "ICC T20 rules apply"
      ],
      "eligibility": "Current college students with valid ID",
      "maxTeams": 16,
      "registrationLink": "https://unstop.com/competitions/cricket-championship"
    }
  ]
}

// Schedule Data Structure (schedule.json)
{
  "days": [
    {
      "date": "2024-03-15",
      "day": "Day 1",
      "events": [
        {
          "time": "09:00 AM",
          "sport": "Cricket",
          "event": "Opening Ceremony",
          "venue": "Main Stadium"
        }
      ]
    }
  ]
}

// Event Configuration
const EVENT_CONFIG = {
  name: "InterCollege Sports Championship 2024",
  tagline: "Compete. Connect. Conquer.",
  startDate: "2024-03-15T09:00:00",
  endDate: "2024-03-20T18:00:00",
  venue: {
    name: "Sports Complex",
    address: "123 University Road",
    coordinates: { lat: 28.7041, lng: 77.1025 }
  },
  unstopBaseUrl: "https://unstop.com/competitions/",
  socialLinks: {
    instagram: "https://instagram.com/sportclub",
    facebook: "https://facebook.com/sportclub",
    whatsapp: "https://chat.whatsapp.com/invite-link"
  }
};
```

### Implementation Tasks

```yaml
Task 1: Setup Project Structure and Build System
- Initialize project with folder structure
- Setup Tailwind CSS with custom sports theme colors
- Configure live-server for development
- Create base HTML template with SEO meta tags
- Setup responsive navigation component

Task 2: Implement Home Page with Hero Section
- Create animated hero section with event branding
- Implement countdown timer component
- Add "Register Now" CTA with Unstop redirect
- Include highlights carousel for key features
- Add social proof section (past participants/colleges)

Task 3: Build About Event Page
- Create content sections with scroll animations
- Add organizing committee information
- Include prize pool and benefits
- Implement testimonials from past events
- Add sponsor logos section

Task 4: Develop Sports & Activities Showcase
- Create dynamic sports cards from JSON data
- Implement filter/search functionality
- Add modal popups for detailed rules
- Include registration CTAs per sport
- Create responsive grid layout

Task 5: Create Interactive Schedule Page
- Build schedule table from JSON data
- Implement day-wise filtering
- Add download PDF functionality
- Create print-friendly CSS
- Optional: Google Sheets integration

Task 6: Setup Gallery with Lazy Loading
- Implement image gallery with categories
- Add Swiper.js for touch navigation
- Setup lazy loading for performance
- Include Instagram feed integration
- Add lightbox for full-screen view

Task 7: Build Contact Page with Map
- Embed Google Maps with venue marker
- Add contact form (forwards to email)
- Include emergency contact numbers
- Add FAQ section
- Social media links grid

Task 8: Implement Cross-cutting Features
- Add PWA manifest for installability
- Implement service worker for offline
- Setup Google Analytics
- Add cookie consent banner
- Implement dark mode toggle

Task 9: Performance Optimization
- Minify CSS/JS for production
- Optimize images (WebP conversion)
- Setup CDN for static assets
- Implement critical CSS inlining
- Add resource hints (preconnect, prefetch)

Task 10: Testing and Launch Preparation
- Cross-browser testing (Chrome, Firefox, Safari, Edge)
- Mobile responsiveness testing
- Accessibility audit with axe DevTools
- SEO audit with Lighthouse
- Setup hosting (Netlify/Vercel recommended)
```

### Key Implementation Code

```javascript
// Countdown Timer Implementation
class CountdownTimer {
  constructor(targetDate, elementId) {
    this.targetDate = new Date(targetDate).getTime();
    this.element = document.getElementById(elementId);
    this.init();
  }

  init() {
    this.update();
    setInterval(() => this.update(), 1000);
  }

  update() {
    const now = new Date().getTime();
    const distance = this.targetDate - now;

    if (distance < 0) {
      this.element.innerHTML = "<span class='text-green-500'>Event Started!</span>";
      return;
    }

    const days = Math.floor(distance / (1000 * 60 * 60 * 24));
    const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((distance % (1000 * 60)) / 1000);

    this.element.innerHTML = `
      <div class="flex gap-4">
        <div class="text-center">
          <div class="text-4xl font-bold">${days}</div>
          <div class="text-sm">Days</div>
        </div>
        <div class="text-center">
          <div class="text-4xl font-bold">${hours}</div>
          <div class="text-sm">Hours</div>
        </div>
        <div class="text-center">
          <div class="text-4xl font-bold">${minutes}</div>
          <div class="text-sm">Minutes</div>
        </div>
        <div class="text-center">
          <div class="text-4xl font-bold">${seconds}</div>
          <div class="text-sm">Seconds</div>
        </div>
      </div>
    `;
  }
}

// Sports Cards Dynamic Generation
async function loadSports() {
  try {
    const response = await fetch('/data/sports.json');
    const data = await response.json();
    const container = document.getElementById('sports-grid');
    
    data.sports.forEach(sport => {
      const card = createSportCard(sport);
      container.appendChild(card);
    });
  } catch (error) {
    console.error('Failed to load sports:', error);
  }
}

function createSportCard(sport) {
  const card = document.createElement('div');
  card.className = 'sport-card bg-white rounded-lg shadow-lg overflow-hidden transform transition hover:scale-105';
  card.innerHTML = `
    <img src="${sport.image}" alt="${sport.name}" class="w-full h-48 object-cover lazy-load">
    <div class="p-6">
      <h3 class="text-2xl font-bold mb-2">${sport.icon} ${sport.name}</h3>
      <p class="text-gray-600 mb-4">${sport.description}</p>
      <button onclick="showSportDetails('${sport.id}')" 
              class="text-blue-600 hover:text-blue-800 mr-4">
        View Rules
      </button>
      <a href="${sport.registrationLink}" 
         target="_blank" 
         class="bg-green-500 text-white px-4 py-2 rounded hover:bg-green-600">
        Register on Unstop
      </a>
    </div>
  `;
  return card;
}

// Schedule PDF Download
function downloadSchedulePDF() {
  // Simple approach - link to pre-generated PDF
  const link = document.createElement('a');
  link.href = '/assets/downloads/schedule.pdf';
  link.download = 'Competition_Schedule_2024.pdf';
  link.click();
}

// Lazy Loading for Gallery
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      img.classList.remove('lazy-load');
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('.lazy-load').forEach(img => {
  imageObserver.observe(img);
});
```

### Integration Points
```yaml
EXTERNAL SERVICES:
  - Unstop: Registration links (no API needed)
  - Google Maps: Embedded venue location
  - Google Analytics: Event tracking
  - Instagram: Gallery feed widget
  - WhatsApp: Group invite link
  
HOSTING:
  - Recommended: Netlify/Vercel (free tier)
  - Alternative: GitHub Pages
  - CDN: Cloudflare for assets
  
ENVIRONMENT:
  - No .env needed (all public data)
  - Configuration in EVENT_CONFIG object
  - Update sports.json and schedule.json for content
```

## Validation & Testing

### Level 1: Code Quality
```bash
# HTML Validation
# Use W3C Validator: https://validator.w3.org/

# CSS Validation  
# Use W3C CSS Validator: https://jigsaw.w3.org/css-validator/

# JavaScript Linting
npx eslint assets/js/*.js --fix
```

### Level 2: Performance Testing
```bash
# Lighthouse Audit (in Chrome DevTools)
# Target scores:
# - Performance: >90
# - Accessibility: >95
# - Best Practices: >90
# - SEO: >95

# Page Speed Insights
# Test at: https://pagespeed.web.dev/
```

### Level 3: Cross-browser Testing
```
Manual Testing Checklist:
- [ ] Chrome (Desktop + Mobile)
- [ ] Firefox
- [ ] Safari (Mac + iOS)
- [ ] Edge
- [ ] Samsung Internet

Features to Test:
- [ ] Countdown timer updates
- [ ] Navigation menu (mobile hamburger)
- [ ] Sports cards hover effects
- [ ] Gallery swiper touch events
- [ ] Unstop registration links
- [ ] Schedule table responsiveness
- [ ] Map embed loads correctly
```

### Level 4: User Flow Testing
```
Critical User Paths:
1. Home → Sports → Unstop Registration
2. Home → Schedule → Download PDF
3. Home → Gallery → View Photos
4. Home → Contact → Find Venue

Each path should:
- Load in <3 seconds
- Work on mobile
- Have clear CTAs
- Handle errors gracefully
```

## Final Validation Checklist
- [ ] All pages responsive (test at 320px, 768px, 1920px)
- [ ] Countdown timer shows correct time
- [ ] All Unstop registration links work
- [ ] Schedule PDF downloads correctly
- [ ] Images optimized (<100KB for thumbnails)
- [ ] Social media links open in new tabs
- [ ] Google Maps shows correct venue
- [ ] Contact form sends emails (if implemented)
- [ ] Gallery images lazy load
- [ ] SEO meta tags on all pages
- [ ] Favicon displays correctly
- [ ] 404 page exists
- [ ] robots.txt and sitemap.xml configured
- [ ] Analytics tracking code installed
- [ ] SSL certificate active (https://)

## Deployment Guide

### Quick Deploy to Netlify
```bash
# 1. Build production files
npm run build  # If using build tools

# 2. Deploy via Netlify CLI
npx netlify-cli deploy --prod --dir=.

# Or drag-and-drop folder to netlify.com
```

### Custom Domain Setup
```yaml
DNS Records:
- Type: A
  Name: @
  Value: Netlify/Vercel IP
  
- Type: CNAME
  Name: www
  Value: your-site.netlify.app
```

---

## Anti-Patterns to Avoid
- ❌ Don't hardcode dates - use configuration object
- ❌ Don't skip image optimization - causes slow loading
- ❌ Don't forget mobile testing - 60%+ users are mobile
- ❌ Don't use synchronous scripts - blocks page rendering
- ❌ Don't skip meta tags - hurts SEO and sharing
- ❌ Don't ignore accessibility - limits audience reach
- ❌ Don't overcomplicate - keep it maintainable

## Future Enhancements (Post-Launch)
- Live score updates during events
- Participant dashboard (with Unstop API)
- Push notifications for schedule changes
- Live streaming integration
- Multi-language support
- Automated social media posts
- QR code check-in system

## Confidence Score: 9/10

High confidence because:
- Static site approach minimizes complexity
- Unstop handles complex registration/payment logic
- Clear separation of content and functionality
- Well-established patterns and libraries used
- No backend reduces potential failure points

Minor uncertainty only around specific Unstop integration details, but redirect approach is straightforward.