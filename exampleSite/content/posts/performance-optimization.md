---
title: "Web Performance Optimization: Speed Up Your Site"
description: "Essential techniques for optimizing web performance. Learn how to make your website faster with practical tips and modern best practices."
date: 2024-01-12T16:45:00Z
lastmod: 2024-01-12T16:45:00Z
draft: false
author: "Hugo Base Theme"
categories: ["Performance", "Web Development"]
tags: ["performance", "optimization", "speed", "core-web-vitals", "lighthouse"]
featured_image: "/images/posts/performance.jpg"
featured_image_alt: "Website speed optimization dashboard"
toc: true
---

Website performance directly impacts user experience, SEO rankings, and conversion rates. A fast website keeps users engaged, while a slow one drives them away. Let's explore proven techniques to optimize your site's performance.

## Why Performance Matters

### User Experience Impact
- **53% of users** abandon sites that take longer than 3 seconds to load
- **1-second delay** can reduce conversions by 7%
- **Fast sites** feel more trustworthy and professional

### Business Impact
- **Better SEO rankings**: Google uses page speed as a ranking factor
- **Higher conversion rates**: Faster sites convert better
- **Reduced bounce rates**: Users stay longer on fast sites
- **Lower hosting costs**: Efficient sites use fewer resources

## Core Web Vitals

Google's Core Web Vitals are essential metrics for user experience:

### Largest Contentful Paint (LCP)
Measures loading performance. Should occur within **2.5 seconds**.

```javascript
// Measure LCP
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    console.log('LCP:', entry.startTime);
  }
}).observe({entryTypes: ['largest-contentful-paint']});
```

### First Input Delay (FID)
Measures interactivity. Should be less than **100 milliseconds**.

```javascript
// Measure FID
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    console.log('FID:', entry.processingStart - entry.startTime);
  }
}).observe({entryTypes: ['first-input']});
```

### Cumulative Layout Shift (CLS)
Measures visual stability. Should be less than **0.1**.

```javascript
// Measure CLS
let clsValue = 0;
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    if (!entry.hadRecentInput) {
      clsValue += entry.value;
    }
  }
  console.log('CLS:', clsValue);
}).observe({entryTypes: ['layout-shift']});
```

## Image Optimization

Images often account for 60-70% of page weight. Optimizing them is crucial.

### Modern Image Formats
```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description" loading="lazy">
</picture>
```

### Responsive Images
```html
<img
  src="small.jpg"
  srcset="small.jpg 480w, medium.jpg 800w, large.jpg 1200w"
  sizes="(max-width: 480px) 100vw, (max-width: 800px) 50vw, 25vw"
  alt="Responsive image"
  loading="lazy"
>
```

### Lazy Loading
```html
<!-- Native lazy loading -->
<img src="image.jpg" alt="Description" loading="lazy">

<!-- Intersection Observer for older browsers -->
<img data-src="image.jpg" alt="Description" class="lazy">
```

```javascript
// Lazy loading with Intersection Observer
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      img.classList.remove('lazy');
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('img[data-src]').forEach(img => {
  imageObserver.observe(img);
});
```

## CSS Optimization

### Critical CSS
Inline critical CSS to prevent render-blocking:

```html
<head>
  <style>
    /* Critical CSS for above-the-fold content */
    body { font-family: sans-serif; margin: 0; }
    .header { background: #333; color: white; padding: 1rem; }
    .hero { min-height: 50vh; display: flex; align-items: center; }
  </style>

  <!-- Load non-critical CSS asynchronously -->
  <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="styles.css"></noscript>
</head>
```

### CSS Minification
```css
/* Before minification */
.button {
  background-color: #007bff;
  border: none;
  padding: 12px 24px;
  border-radius: 4px;
  color: white;
  cursor: pointer;
}

/* After minification */
.button{background-color:#007bff;border:none;padding:12px 24px;border-radius:4px;color:white;cursor:pointer}
```

### Remove Unused CSS
```javascript
// Using PurgeCSS
const purgecss = require('@fullhuman/postcss-purgecss');

module.exports = {
  plugins: [
    purgecss({
      content: ['./src/**/*.html', './src/**/*.js'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
    })
  ]
};
```

## JavaScript Optimization

### Code Splitting
```javascript
// Dynamic imports for code splitting
const loadModule = async () => {
  const { heavyFunction } = await import('./heavy-module.js');
  return heavyFunction();
};

// Route-based splitting
const HomePage = lazy(() => import('./HomePage'));
const AboutPage = lazy(() => import('./AboutPage'));
```

### Tree Shaking
```javascript
// Import only what you need
import { debounce } from 'lodash-es';

// Instead of importing everything
import _ from 'lodash';
```

### Minification and Compression
```javascript
// Webpack configuration
module.exports = {
  optimization: {
    minimize: true,
    minimizer: [
      new TerserPlugin({
        terserOptions: {
          compress: {
            drop_console: true,
          },
        },
      }),
    ],
  },
};
```

## Resource Loading Optimization

### Preloading Critical Resources
```html
<!-- Preload critical resources -->
<link rel="preload" href="critical.css" as="style">
<link rel="preload" href="hero-image.jpg" as="image">
<link rel="preload" href="main.js" as="script">

<!-- Prefetch resources for next page -->
<link rel="prefetch" href="next-page.html">
<link rel="prefetch" href="next-page.css">
```

### DNS Prefetching
```html
<!-- Resolve DNS early for external resources -->
<link rel="dns-prefetch" href="//fonts.googleapis.com">
<link rel="dns-prefetch" href="//api.example.com">
<link rel="dns-prefetch" href="//cdn.example.com">
```

### Resource Hints
```html
<!-- Preconnect to important third-party origins -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Module preload for ES modules -->
<link rel="modulepreload" href="app.js">
```

## Font Optimization

### Font Loading Strategies
```css
/* Font display strategies */
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* Show fallback, then swap */
}

/* Alternative strategies */
font-display: block;    /* Block text, then show custom font */
font-display: fallback; /* Brief block, then fallback if not loaded */
font-display: optional; /* Use custom font only if cached */
```

### Preloading Fonts
```html
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
```

### Variable Fonts
```css
/* Single file for multiple weights/styles */
@font-face {
  font-family: 'Inter';
  src: url('Inter-Variable.woff2') format('woff2');
  font-weight: 100 900;
  font-style: normal;
}

.text {
  font-family: 'Inter', sans-serif;
  font-weight: 450; /* Any value between 100-900 */
}
```

## Caching Strategies

### HTTP Caching Headers
```nginx
# Nginx configuration
location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
  expires 1y;
  add_header Cache-Control "public, immutable";
}

location ~* \.(html)$ {
  expires 1h;
  add_header Cache-Control "public, must-revalidate";
}
```

### Service Worker Caching
```javascript
// Service worker for caching
const CACHE_NAME = 'v1';
const urlsToCache = [
  '/',
  '/styles.css',
  '/script.js',
  '/offline.html'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        return response || fetch(event.request);
      })
  );
});
```

## Performance Monitoring

### Real User Monitoring (RUM)
```javascript
// Web Vitals library
import {getCLS, getFID, getFCP, getLCP, getTTFB} from 'web-vitals';

function sendToAnalytics(metric) {
  // Send to your analytics service
  gtag('event', metric.name, {
    value: Math.round(metric.name === 'CLS' ? metric.value * 1000 : metric.value),
    event_label: metric.id,
  });
}

getCLS(sendToAnalytics);
getFID(sendToAnalytics);
getFCP(sendToAnalytics);
getLCP(sendToAnalytics);
getTTFB(sendToAnalytics);
```

### Performance Observer
```javascript
// Monitor long tasks
const observer = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    if (entry.duration > 50) {
      console.warn('Long task detected:', entry);
    }
  }
});

observer.observe({entryTypes: ['longtask']});
```

## Build Tool Optimization

### Webpack Optimization
```javascript
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all',
        },
      },
    },
  },
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
    },
  },
};
```

### Vite Configuration
```javascript
// vite.config.js
export default {
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['lodash', 'date-fns'],
        },
      },
    },
  },
  optimizeDeps: {
    include: ['react', 'react-dom'],
  },
};
```

## Server-Side Optimization

### Compression
```nginx
# Gzip compression
gzip on;
gzip_vary on;
gzip_min_length 1024;
gzip_types
  text/plain
  text/css
  text/xml
  text/javascript
  application/javascript
  application/xml+rss
  application/json;
```

### HTTP/2 Server Push
```nginx
# HTTP/2 Server Push
location = /index.html {
  http2_push /styles.css;
  http2_push /script.js;
}
```

### CDN Configuration
```javascript
// CloudFront configuration
const distribution = {
  Origins: [{
    DomainName: 'example.com',
    CustomOriginConfig: {
      HTTPPort: 80,
      HTTPSPort: 443,
      OriginProtocolPolicy: 'https-only'
    }
  }],
  DefaultCacheBehavior: {
    Compress: true,
    ViewerProtocolPolicy: 'redirect-to-https'
  }
};
```

## Performance Budget

### Setting Budgets
```json
{
  "budget": [
    {
      "path": "/**",
      "timings": [
        {
          "metric": "interactive",
          "budget": 5000
        },
        {
          "metric": "first-meaningful-paint",
          "budget": 2000
        }
      ],
      "resourceSizes": [
        {
          "resourceType": "script",
          "budget": 170
        },
        {
          "resourceType": "total",
          "budget": 300
        }
      ]
    }
  ]
}
```

### Lighthouse CI
```yaml
# .github/workflows/lighthouse.yml
name: Lighthouse CI
on: [push]
jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Lighthouse CI
        run: |
          npm install -g @lhci/cli@0.8.x
          lhci autorun
```

## Testing Tools

### Lighthouse
```bash
# Command line Lighthouse
npm install -g lighthouse
lighthouse https://example.com --output html --output-path ./report.html
```

### WebPageTest
```javascript
// WebPageTest API
const WebPageTest = require('webpagetest');
const wpt = new WebPageTest('www.webpagetest.org', 'API_KEY');

wpt.runTest('https://example.com', {
  location: 'Dulles:Chrome',
  runs: 3,
  firstViewOnly: false
}, (err, data) => {
  console.log(data);
});
```

## Quick Wins Checklist

- [ ] Enable gzip/brotli compression
- [ ] Optimize and compress images
- [ ] Minify CSS, JavaScript, and HTML
- [ ] Use a Content Delivery Network (CDN)
- [ ] Enable browser caching
- [ ] Remove unused CSS and JavaScript
- [ ] Lazy load images and videos
- [ ] Use modern image formats (WebP, AVIF)
- [ ] Preload critical resources
- [ ] Optimize web fonts
- [ ] Reduce HTTP requests
- [ ] Use HTTP/2
- [ ] Implement service worker caching
- [ ] Monitor Core Web Vitals

## Conclusion

Web performance optimization is an ongoing process that requires attention to multiple areas: images, CSS, JavaScript, fonts, caching, and server configuration. Start with the biggest impact items like image optimization and compression, then gradually implement more advanced techniques.

Remember to measure before and after optimizations to ensure they're actually improving performance. Tools like Lighthouse, WebPageTest, and real user monitoring help you understand your site's performance and identify areas for improvement.

Fast websites provide better user experiences, rank higher in search results, and convert better. The investment in performance optimization pays dividends in user satisfaction and business results. ⚡
